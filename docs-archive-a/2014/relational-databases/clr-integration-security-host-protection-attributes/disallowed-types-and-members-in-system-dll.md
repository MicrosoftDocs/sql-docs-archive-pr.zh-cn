---
title: System.dll 中不允许的类型和成员 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- host protection attributes [CLR integration]
- common language runtime [SQL Server], host protection attributes
ms.assetid: 27b550cd-dd3d-4263-bd97-0f0dec1215fd
author: rothja
ms.author: jroth
ms.openlocfilehash: 50469270c8572328468f2b5cf3072c009e76ce0b
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87691263"
---
# <a name="disallowed-types-and-members-in-systemdll"></a>System.dll 中禁用的类型和成员
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]公共语言集成 (CLR) 编程不允许使用具有、、、、、、、 `HostProtectionAttribute` `System.Security.Permissions.HostProtectionResource` `ExternalProcessMgmt` `ExternalThreading` `MayLeakOnAbort` `SecurityInfrastructure` `SelfAffectingProcessMgmnt` `SelfAffectingThreading` **SharedState**、 `Synchronization` 或 `UI` 值指定枚举的类型或成员。 下表列出了不允许其宿主保护属性 (HPA) 值的 System.dll 程序集的成员和类型。  
  
> [!NOTE]  
>  此列表是通过支持的程序集生成的。 有关详细信息，请参阅[支持的 .NET Framework 库](../clr-integration/database-objects/supported-net-framework-libraries.md)。  
  
|类型或成员|HPA 值|  
|--------------------|--------------------|  
|Microsoft.Win32.NativeMethods|MayLeakOnAbort|  
|Microsoft.Win32.PowerModeChangedEventArgs|MayLeakOnAbort|  
|Microsoft.Win32.PowerModeChangedEventHandler|MayLeakOnAbort|  
|Microsoft.Win32.SafeHandles.SafeEventHandle|MayLeakOnAbort|  
|Microsoft.Win32.SafeHandles.SafeEventLogReadHandle|MayLeakOnAbort|  
|Microsoft.Win32.SafeHandles.SafeEventLogWriteHandle|MayLeakOnAbort|  
|Microsoft.Win32.SafeHandles.SafeFileMappingHandle|MayLeakOnAbort|  
|Microsoft.Win32.SafeHandles.SafeFileMapViewHandle|MayLeakOnAbort|  
|Microsoft.Win32.SafeHandles.SafeLibraryHandle|MayLeakOnAbort|  
|Microsoft.Win32.SafeHandles.SafeLocalMemHandle|MayLeakOnAbort|  
|Microsoft.Win32.SafeHandles.SafeProcessHandle|MayLeakOnAbort|  
|Microsoft.Win32.SafeHandles.SafeTimerHandle|MayLeakOnAbort|  
|Microsoft.Win32.SafeHandles.SafeUserTokenHandle|MayLeakOnAbort|  
|Microsoft.Win32.SafeNativeMethods|MayLeakOnAbort|  
|Microsoft.Win32.SessionEndedEventArgs|MayLeakOnAbort|  
|Microsoft.Win32.SessionEndedEventHandler|MayLeakOnAbort|  
|Microsoft.Win32.SessionEndingEventArgs|MayLeakOnAbort|  
|Microsoft.Win32.SessionEndingEventHandler|MayLeakOnAbort|  
|Microsoft.Win32.SessionSwitchEventArgs|MayLeakOnAbort|  
|Microsoft.Win32.SessionSwitchEventHandler|MayLeakOnAbort|  
|Microsoft.Win32.SystemEvents|MayLeakOnAbort|  
|Microsoft.Win32.TimerElapsedEventArgs|MayLeakOnAbort|  
|Microsoft.Win32.TimerElapsedEventHandler|MayLeakOnAbort|  
|Microsoft.Win32.UnsafeNativeMethods|MayLeakOnAbort|  
|Microsoft.Win32.UserPreferenceChangedEventArgs|MayLeakOnAbort|  
|Microsoft.Win32.UserPreferenceChangedEventHandler|MayLeakOnAbort|  
|Microsoft.Win32.UserPreferenceChangingEventArgs|MayLeakOnAbort|  
|Microsoft.Win32.UserPreferenceChangingEventHandler|MayLeakOnAbort|  
|System.ComponentModel.AddingNewEventArgs|SharedState|  
|System.ComponentModel.AddingNewEventHandler|SharedState|  
|System.ComponentModel.ArrayConverter|SharedState|  
|System.ComponentModel.ArraySubsetEnumerator|SharedState|  
|System.ComponentModel.AsyncCompletedEventArgs|SharedState|  
|System.ComponentModel.AsyncCompletedEventHandler|SharedState|  
|System.ComponentModel.AsyncOperation|SharedState|  
|System.ComponentModel.AsyncOperationManager|SharedState|  
|System.ComponentModel.AttributeCollection|同步|  
|System.ComponentModel.BackgroundWorker|SharedState|  
|System.ComponentModel.BaseNumberConverter|SharedState|  
|System.ComponentModel.BindingList|SharedState|  
|System.ComponentModel.BooleanConverter|SharedState|  
|System.ComponentModel.ByteConverter|SharedState|  
|System.ComponentModel.CancelEventArgs|SharedState|  
|System.ComponentModel.CancelEventHandler|SharedState|  
|System.ComponentModel.CharConverter|SharedState|  
|System.ComponentModel.CollectionChangeEventArgs|SharedState|  
|System.ComponentModel.CollectionChangeEventHandler|SharedState|  
|System.ComponentModel.CollectionConverter|SharedState|  
|System.ComponentModel.CompModSwitches|SharedState|  
|System.ComponentModel.ComponentCollection|同步|  
|System.ComponentModel.ComponentConverter|SharedState|  
|System.ComponentModel.ComponentEditor|SharedState|  
|System.ComponentModel.ComponentResourceManager|SharedState|  
|System.ComponentModel.Container|SharedState|  
|System.ComponentModel.ContainerFilterService|SharedState|  
|System.ComponentModel.CultureInfoConverter|SharedState|  
|System.ComponentModel.CustomTypeDescriptor|SharedState|  
|System.ComponentModel.DateTimeConverter|SharedState|  
|System.ComponentModel.DecimalConverter|SharedState|  
|System.ComponentModel.DelegatingTypeDescriptionProvider|SharedState|  
|System.ComponentModel.Design.ActiveDesignerEventArgs|SharedState|  
|System.ComponentModel.Design.ActiveDesignerEventHandler|SharedState|  
|System.ComponentModel.Design.CheckoutException|SharedState|  
|System.ComponentModel.Design.CommandID|SharedState|  
|System.ComponentModel.Design.ComponentChangedEventArgs|SharedState|  
|System.ComponentModel.Design.ComponentChangedEventHandler|SharedState|  
|System.ComponentModel.Design.ComponentChangingEventArgs|SharedState|  
|System.ComponentModel.Design.ComponentChangingEventHandler|SharedState|  
|System.ComponentModel.Design.ComponentEventArgs|SharedState|  
|System.ComponentModel.Design.ComponentEventHandler|SharedState|  
|System.ComponentModel.Design.ComponentRenameEventArgs|SharedState|  
|System.ComponentModel.Design.ComponentRenameEventHandler|SharedState|  
|System.ComponentModel.Design.DesignerCollection|SharedState|  
|System.ComponentModel.Design.DesignerEventArgs|SharedState|  
|System.ComponentModel.Design.DesignerEventHandler|SharedState|  
|System.ComponentModel.Design.DesignerOptionService|SharedState|  
|System.ComponentModel.Design.DesignerTransaction|SharedState|  
|System.ComponentModel.Design.DesignerTransactionCloseEventArgs|SharedState|  
|System.ComponentModel.Design.DesignerTransactionCloseEventHandler|SharedState|  
|System.ComponentModel.Design.DesignerVerb|SharedState|  
|System.ComponentModel.Design.DesignerVerbCollection|SharedState|  
|System.ComponentModel.Design.DesigntimeLicenseContext|SharedState|  
|System.ComponentModel.Design.DesigntimeLicenseContextSerializer|SharedState|  
|System.ComponentModel.Design.MenuCommand|SharedState|  
|System.ComponentModel.Design.RuntimeLicenseContext|SharedState|  
|System.ComponentModel.Design.Serialization.ComponentSerializationService|SharedState|  
|System.ComponentModel.Design.Serialization.ContextStack|SharedState|  
|System.ComponentModel.Design.Serialization.DesignerLoader|SharedState|  
|System.ComponentModel.Design.Serialization.InstanceDescriptor|SharedState|  
|System.ComponentModel.Design.Serialization.MemberRelationshipService|SharedState|  
|System.ComponentModel.Design.Serialization.ResolveNameEventArgs|SharedState|  
|System.ComponentModel.Design.Serialization.ResolveNameEventHandler|SharedState|  
|System.ComponentModel.Design.Serialization.SerializationStore|SharedState|  
|System.ComponentModel.Design.ServiceContainer|SharedState|  
|System.ComponentModel.Design.ServiceCreatorCallback|SharedState|  
|System.ComponentModel.Design.StandardCommands|SharedState|  
|System.ComponentModel.Design.StandardToolWindows|SharedState|  
|System.ComponentModel.DoubleConverter|SharedState|  
|System.ComponentModel.DoWorkEventArgs|SharedState|  
|System.ComponentModel.DoWorkEventHandler|SharedState|  
|System.ComponentModel.EnumConverter|SharedState|  
|System.ComponentModel.EventDescriptor|SharedState|  
|System.ComponentModel.EventDescriptorCollection|同步|  
|System.ComponentModel.EventHandlerList|SharedState|  
|System.ComponentModel.ExpandableObjectConverter|SharedState|  
|System.ComponentModel.ExtendedPropertyDescriptor|SharedState|  
|System.ComponentModel.GuidConverter|SharedState|  
|System.ComponentModel.HandledEventArgs|SharedState|  
|System.ComponentModel.HandledEventHandler|SharedState|  
|System.ComponentModel.InstanceCreationEditor|SharedState|  
|System.ComponentModel.Int16Converter|SharedState|  
|System.ComponentModel.Int32Converter|SharedState|  
|System.ComponentModel.Int64Converter|SharedState|  
|System.ComponentModel.IntSecurity|SharedState|  
|System.ComponentModel.InvalidAsynchronousStateException|SharedState|  
|System.ComponentModel.InvalidEnumArgumentException|SharedState|  
|System.ComponentModel.ISynchronizeInvoke.BeginInvoke ()|ExternalThreading，Synchronization|  
|System.ComponentModel.License|SharedState|  
|System.ComponentModel.LicenseContext|SharedState|  
|System.ComponentModel.LicenseException|SharedState|  
|System.ComponentModel.LicenseManager|ExternalProcessMgmt|  
|System.ComponentModel.LicenseProvider|SharedState|  
|System.ComponentModel.LicFileLicenseProvider|SharedState|  
|System.ComponentModel.ListChangedEventArgs|SharedState|  
|System.ComponentModel.ListChangedEventHandler|SharedState|  
|System.ComponentModel.ListSortDescription|SharedState|  
|System.ComponentModel.ListSortDescriptionCollection|SharedState|  
|System.ComponentModel.MaskedTextProvider|SharedState|  
|System.ComponentModel.MemberDescriptor|SharedState|  
|System.ComponentModel.MultilineStringConverter|SharedState|  
|System.ComponentModel.NestedContainer|SharedState|  
|System.ComponentModel.NullableConverter|SharedState|  
|System.ComponentModel.ProgressChangedEventArgs|SharedState|  
|System.ComponentModel.ProgressChangedEventHandler|SharedState|  
|System.ComponentModel.PropertyChangedEventArgs|SharedState|  
|System.ComponentModel.PropertyChangedEventHandler|SharedState|  
|System.ComponentModel.PropertyDescriptor|SharedState|  
|System.ComponentModel.PropertyDescriptorCollection|同步|  
|System.ComponentModel.ReferenceConverter|SharedState|  
|System.ComponentModel.ReflectEventDescriptor|SharedState|  
|System.ComponentModel.ReflectPropertyDescriptor|SharedState|  
|System.ComponentModel.ReflectTypeDescriptionProvider|SharedState|  
|System.ComponentModel.RefreshEventArgs|SharedState|  
|System.ComponentModel.RefreshEventHandler|SharedState|  
|System.ComponentModel.RunWorkerCompletedEventArgs|SharedState|  
|System.ComponentModel.RunWorkerCompletedEventHandler|SharedState|  
|System.ComponentModel.SByteConverter|SharedState|  
|System.ComponentModel.SingleConverter|SharedState|  
|System.ComponentModel.StringConverter|SharedState|  
|System.ComponentModel.SyntaxCheck|SharedState|  
|System.ComponentModel.TimeSpanConverter|SharedState|  
|System.ComponentModel.TypeConverter|SharedState|  
|System.ComponentModel.TypeDescriptionProvider|SharedState|  
|System.ComponentModel.TypeDescriptor|SharedState|  
|System.ComponentModel.TypeListConverter|SharedState|  
|System.ComponentModel.UInt16Converter|SharedState|  
|System.ComponentModel.UInt32Converter|SharedState|  
|System.ComponentModel.UInt64Converter|SharedState|  
|System.ComponentModel.WarningException|SharedState|  
|System.ComponentModel.WeakHashtable|SharedState|  
|System.ComponentModel.Win32Exception|SharedState|  
|System.Diagnostics.ConsoleTraceListener|同步|  
|System.Diagnostics.Debug.get_Listeners ()|SharedState|  
|System.Diagnostics.DefaultTraceListener|同步|  
|System.Diagnostics.DelimitedListTraceListener|同步|  
|System.Diagnostics.EventLog.get_SynchronizingObject ()|同步|  
|System.Diagnostics.EventLogTraceListener|同步|  
|System.Diagnostics.PerformanceCounter|SharedState, Synchronization|  
|System.Diagnostics.PerformanceCounterCategory|SharedState, Synchronization|  
|System.Diagnostics.Process|SelfAffectingProcessMgmt、ExternalProcessMgmt、SharedState、Synchronization|  
|System.Diagnostics.ProcessStartInfo|SelfAffectingProcessMgmt、SharedState|  
|System.Diagnostics.ProcessThread|SelfAffectingThreading、SelfAffectingProcessMgmt|  
|System.Diagnostics.SharedPerformanceCounter|SharedState, Synchronization|  
|System.Diagnostics.TextWriterTraceListener|同步|  
|System.Diagnostics.Trace.get_Listeners()|SharedState|  
|System.Diagnostics.TraceListener|同步|  
|System.Diagnostics.XmlWriterTraceListener|同步|  
|System.IO.Compression.DeflateStream.BeginRead()|ExternalThreading|  
|System.IO.Compression.DeflateStream.BeginWrite()|ExternalThreading|  
|System.IO.Compression.GZipStream.BeginRead()|ExternalThreading|  
|System.IO.Compression.GZipStream.BeginWrite()|ExternalThreading|  
|System.IO.Ports.SerialStream.BeginRead()|ExternalThreading|  
|System.IO.Ports.SerialStream.BeginWrite()|ExternalThreading|  
|System.Media.SoundPlayer|UI|  
|System.Media.SystemSound|UI|  
|System.Media.SystemSounds|UI|  
|System.Net.ConnectStream.BeginRead()|ExternalThreading|  
|System.Net.ConnectStream.BeginWrite()|ExternalThreading|  
|System.Net.Dns.BeginGetHostAddresses()|ExternalThreading|  
|System.Net.Dns.BeginGetHostByName()|ExternalThreading|  
|System.Net.Dns.BeginGetHostEntry()|ExternalThreading|  
|System.Net.Dns.BeginResolve()|ExternalThreading|  
|System.Net.FileWebRequest.BeginGetRequestStream()|ExternalThreading|  
|System.Net.FileWebRequest.BeginGetResponse()|ExternalThreading|  
|System.Net.FtpDataStream.BeginRead()|ExternalThreading|  
|System.Net.FtpDataStream.BeginWrite()|ExternalThreading|  
|System.Net.FtpWebRequest.BeginGetRequestStream()|ExternalThreading|  
|System.Net.FtpWebRequest.BeginGetResponse()|ExternalThreading|  
|System.Net.HttpListener.BeginGetContext()|ExternalThreading|  
|System.Net.HttpRequestStream.BeginRead()|ExternalThreading|  
|System.Net.HttpRequestStream.BeginWrite()|ExternalThreading|  
|System.Net.HttpResponseStream.BeginRead()|ExternalThreading|  
|System.Net.HttpResponseStream.BeginWrite()|ExternalThreading|  
|System.Net.HttpWebRequest.BeginGetRequestStream()|ExternalThreading|  
|System.Net.HttpWebRequest.BeginGetResponse()|ExternalThreading|  
|System.Net.Mail.SmtpClient.SendAsync()|ExternalThreading|  
|System.Net.NetworkInformation.Ping.SendAsync()|ExternalThreading|  
|System.Net.PooledStream.BeginRead()|ExternalThreading|  
|System.Net.PooledStream.BeginWrite()|ExternalThreading|  
|System.Net.Security.NegotiateStream.BeginAuthenticateAsClient()|ExternalThreading|  
|System.Net.Security.NegotiateStream.BeginAuthenticateAsServer()|ExternalThreading|  
|System.Net.Security.NegotiateStream.BeginRead()|ExternalThreading|  
|System.Net.Security.NegotiateStream.BeginWrite()|ExternalThreading|  
|System.Net.Security.SslStream.BeginAuthenticateAsClient()|ExternalThreading|  
|System.Net.Security.SslStream.BeginAuthenticateAsServer()|ExternalThreading|  
|System.Net.Security.SslStream.BeginRead()|ExternalThreading|  
|System.Net.Security.SslStream.BeginWrite()|ExternalThreading|  
|System.Net.Sockets.NetworkStream.BeginRead()|ExternalThreading|  
|System.Net.Sockets.NetworkStream.BeginWrite()|ExternalThreading|  
|System.Net.Sockets.Socket.BeginAccept()|ExternalThreading|  
|System.Net.Sockets.Socket.BeginConnect()|ExternalThreading|  
|System.Net.Sockets.Socket.BeginDisconnect()|ExternalThreading|  
|System.Net.Sockets.Socket.BeginReceive()|ExternalThreading|  
|System.Net.Sockets.Socket.BeginReceiveFrom()|ExternalThreading|  
|System.Net.Sockets.Socket.BeginSend()|ExternalThreading|  
|System.Net.Sockets.Socket.BeginSendFile()|ExternalThreading|  
|System.Net.Sockets.Socket.BeginSendTo()|ExternalThreading|  
|System.Net.Sockets.TcpClient.BeginConnect()|ExternalThreading|  
|System.Net.Sockets.TcpListener.BeginAcceptSocket()|ExternalThreading|  
|System.Net.Sockets.TcpListener.BeginAcceptTcpClient()|ExternalThreading|  
|System.Net.Sockets.UdpClient.BeginReceive()|ExternalThreading|  
|System.Net.Sockets.UdpClient.BeginSend()|ExternalThreading|  
|System.Net.SpnDictionary.get_SyncRoot()|同步|  
|System.Net.WebClient.DownloadDataAsync()|ExternalThreading|  
|System.Net.WebClient.DownloadFileAsync()|ExternalThreading|  
|System.Net.WebClient.DownloadStringAsync()|ExternalThreading|  
|System.Net.WebClient.OpenReadAsync()|ExternalThreading|  
|System.Net.WebClient.OpenWriteAsync()|ExternalThreading|  
|System.Net.WebClient.UploadDataAsync()|ExternalThreading|  
|System.Net.WebClient.UploadFileAsync()|ExternalThreading|  
|System.Net.WebClient.UploadStringAsync()|ExternalThreading|  
|System.Net.WebClient.UploadValuesAsync()|ExternalThreading|  
|System.Net.WebRequest.BeginGetRequestStream()|ExternalThreading|  
|System.Net.WebRequest.BeginGetResponse()|同步|  
|System.Text.RegularExpressions.Group.Synchronized()|同步|  
|System.Text.RegularExpressions.Match.Synchronized()|同步|  
|System.Text.RegularExpressions.Regex.CompileToAssembly()|MayLeakOnAbort|  
|System.Threading.Semaphore|ExternalThreading，Synchronization|  
|System.Timers.Timer|ExternalThreading，Synchronization|  
|WebClientWriteStream.BeginRead()|ExternalThreading|  
|WebClientWriteStream.BeginWrite()|ExternalThreading|  
  
## <a name="see-also"></a>另请参阅  
 [宿主保护属性和 CLR 集成编程](host-protection-attributes-and-clr-integration-programming.md)   
 [Microsoft.VisualBasic.dll中不允许的类型和成员](disallowed-types-and-members-in-microsoft-visualbasic-dll.md)   
 [mscorlib.dll中不允许的类型和成员](disallowed-types-and-members-in-mscorlib-dll.md)   
 [System.Data.dll中不允许的类型和成员](disallowed-types-and-members-in-system-data-dll.md)   
 [System.Core.dll 中禁用的类型和成员](disallowed-types-and-members-in-system-core-dll.md)  
  
  
