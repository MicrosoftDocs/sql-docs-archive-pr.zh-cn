---
title: 使用脚本任务发送 HTML 邮件 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
dev_langs:
- VB
helpviewer_keywords:
- Send Mail task [Integration Services]
- Script task [Integration Services], examples
- Script task [Integration Services], HTML mail message
ms.assetid: dd2b1eef-b04f-4946-87ab-7bc56bb525ce
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 6c1a967b52a84e1ff9c2e54c48e40f4d149b2dbc
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87682960"
---
# <a name="sending-an-html-mail-message-with-the-script-task"></a>使用脚本任务发送 HTML 邮件消息
  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] SendMail 任务仅支持纯文本格式的邮件消息。 但是，您可以使用脚本任务以及 .NET Framework 的邮件功能轻松发送 HTML 邮件消息。

> [!NOTE]
>  如果希望创建可更方便地重用于多个包的任务，请考虑以此脚本任务示例中的代码为基础，创建自定义任务。 有关详细信息，请参阅 [开发自定义任务](../extending-packages-custom-objects/task/developing-a-custom-task.md)。

## <a name="description"></a>说明
 下面的示例使用 `System.Net.Mail` 命名空间配置和发送 HTML 邮件消息。 该脚本从包变量获取电子邮件的收件人、发件人、主题和正文，然后使用它们创建新 `MailMessag`e，并将其 `IsBodyHtml` 属性设置为 `True`。 接着，该脚本从另一个包变量获取 SMTP 服务器名称，然后初始化 `System.Net.Mail.SmtpClient` 实例，并调用其 `Send` 方法发送 HTML 消息。 该示例将消息发送功能封装到一个可在其他脚本中重用的子例程中。

#### <a name="to-configure-this-script-task-example-without-an-smtp-connection-manager"></a>不使用 SMTP 连接管理器配置此脚本任务示例

1.  创建名为 `HtmlEmailTo`、`HtmlEmailFrom` 和 `HtmlEmailSubject` 的字符串变量，并向它们分配相应的值，以用于有效的测试消息。

2.  创建一个名为 `HtmlEmailBody` 的字符串变量，并向其分配 HTML 标记字符串。 例如：

    ```
    <html><body><h1>Testing</h1><p>This is a <b>test</b> message.</p></body></html>
    ```

3.  创建一个名为 `HtmlEmailServer` 的字符串变量，并向其分配一个可接收匿名传出消息的可用 SMTP 服务器的名称。

4.  将这五个变量全部分配到新脚本任务的 ReadOnlyVariables 属性  。

5.  将 `System.Net` 和 `System.Net.Mail` 命名空间导入到代码中。

 本主题中的示例代码从包变量获取 SMTP 服务器名称。 当然，还可以利用 SMTP 连接管理器封装连接信息，并在代码中从连接管理器提取服务器名称。 SMTP 连接管理器的 <xref:Microsoft.SqlServer.Dts.ManagedConnections.SMTPConn.AcquireConnection%2A> 方法以下列格式返回一个字符串：

 `SmtpServer=smtphost;UseWindowsAuthentication=False;EnableSsl=False;`

 可以使用 `String.Split` 方法将此参数列表从每个分号 (;) 或等号 (=) 处分为一个单独的字符串数组，然后提取该数组的第二个参数 (subscript 1) 作为服务器名称。

#### <a name="to-configure-this-script-task-example-with-an-smtp-connection-manager"></a>使用 SMTP 连接管理器配置此脚本任务示例

1.  通过从 ReadOnlyVariables 列表删除 `HtmlEmailServer` 变量修改先前配置的脚本任务  。

2.  将获取服务器名称的代码行：

    ```
    Dim smtpServer As String = _
      Dts.Variables("HtmlEmailServer").Value.ToString
    ```

     替换为以下代码行：

    ```
    Dim smtpConnectionString As String = _
      DirectCast(Dts.Connections("SMTP Connection Manager").AcquireConnection(Dts.Transaction), String)
    Dim smtpServer As String = _
      smtpConnectionString.Split(New Char() {"="c, ";"c})(1)
    ```

## <a name="code"></a>代码

```vb
Public Sub Main()

  Dim htmlMessageTo As String = _
    Dts.Variables("HtmlEmailTo").Value.ToString
  Dim htmlMessageFrom As String = _
    Dts.Variables("HtmlEmailFrom").Value.ToString
  Dim htmlMessageSubject As String = _
    Dts.Variables("HtmlEmailSubject").Value.ToString
  Dim htmlMessageBody As String = _
    Dts.Variables("HtmlEmailBody").Value.ToString
  Dim smtpServer As String = _
    Dts.Variables("HtmlEmailServer").Value.ToString

  SendMailMessage( _
      htmlMessageTo, htmlMessageFrom, _
      htmlMessageSubject, htmlMessageBody, _
      True, smtpServer)

  Dts.TaskResult = ScriptResults.Success

End Sub

Private Sub SendMailMessage( _
    ByVal SendTo As String, ByVal From As String, _
    ByVal Subject As String, ByVal Body As String, _
    ByVal IsBodyHtml As Boolean, ByVal Server As String)

  Dim htmlMessage As MailMessage
  Dim mySmtpClient As SmtpClient

  htmlMessage = New MailMessage( _
    SendTo, From, Subject, Body)
  htmlMessage.IsBodyHtml = IsBodyHtml

  mySmtpClient = New SmtpClient(Server)
  mySmtpClient.Credentials = CredentialCache.DefaultNetworkCredentials
  mySmtpClient.Send(htmlMessage)

End Sub
```

```csharp
public void Main()
        {

            string htmlMessageTo = Dts.Variables["HtmlEmailTo"].Value.ToString();
            string htmlMessageFrom = Dts.Variables["HtmlEmailFrom"].Value.ToString();
            string htmlMessageSubject = Dts.Variables["HtmlEmailSubject"].Value.ToString();
            string htmlMessageBody = Dts.Variables["HtmlEmailBody"].Value.ToString();
            string smtpServer = Dts.Variables["HtmlEmailServer"].Value.ToString();

            SendMailMessage(htmlMessageTo, htmlMessageFrom, htmlMessageSubject, htmlMessageBody, true, smtpServer);

            Dts.TaskResult = (int)ScriptResults.Success;

        }

        private void SendMailMessage(string SendTo, string From, string Subject, string Body, bool IsBodyHtml, string Server)
        {

            MailMessage htmlMessage;
            SmtpClient mySmtpClient;

            htmlMessage = new MailMessage(SendTo, From, Subject, Body);
            htmlMessage.IsBodyHtml = IsBodyHtml;

            mySmtpClient = new SmtpClient(Server);
            mySmtpClient.Credentials = CredentialCache.DefaultNetworkCredentials;
            mySmtpClient.Send(htmlMessage);

        }
```

![Integration Services 图标 (小型) ](../media/dts-16.gif "集成服务图标（小）")  **随时保持最新 Integration Services**<br /> 若要从 Microsoft 获得最新的下载内容、文章、示例和视频，以及从社区获得所选解决方案，请访问 MSDN 上的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 页：<br /><br /> [访问 MSDN 上的 Integration Services 页](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> 若要获得有关这些更新的自动通知，请订阅该页上提供的 RSS 源。

## <a name="see-also"></a>另请参阅
 [发送邮件任务](../control-flow/send-mail-task.md)


