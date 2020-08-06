---
title: mscorlib.dll 中不允许的类型和成员 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- host protection attributes [CLR integration]
- common language runtime [SQL Server], host protection attributes
ms.assetid: daf82d4b-2f6d-44ca-9148-75193321b6d5
author: rothja
ms.author: jroth
ms.openlocfilehash: b95d6b6606ebbebcfa507f375e90fa41b2f5db00
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87688942"
---
# <a name="disallowed-types-and-members-in-mscorlibdll"></a>mscorlib.dll 中禁用的类型和成员
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]公共语言集成 (CLR) 编程不允许使用具有、、、、、、、 `HostProtectionAttribute` `System.Security.Permissions.HostProtectionResource` `ExternalProcessMgmt` `ExternalThreading` `MayLeakOnAbort` `SecurityInfrastructure` `SelfAffectingProcessMgmnt` `SelfAffectingThreading` **SharedState**、 `Synchronization` 或 `UI` 值指定枚举的类型或成员。 下表列出了宿主保护属性 (HPA) 值被禁用的 mscorlib.dll 程序集的成员和类型。  
  
> [!NOTE]  
>  此列表是通过支持的程序集生成的。 有关详细信息，请参阅[支持的 .NET Framework 库](../clr-integration/database-objects/supported-net-framework-libraries.md)。  
  
|类型或成员|HPA 值|  
|--------------------|--------------------|  
|SyncStream.BeginRead()|ExternalThreading|  
|SyncStream.BeginWrite()|ExternalThreading|  
|System.Collections.ArrayList.Synchronized()|同步|  
|System.Collections.Hashtable.Synchronized()|同步|  
|System.Collections.Queue.Synchronized()|同步|  
|System.Collections.SortedList.Synchronized()|同步|  
|System.Collections.Stack.Synchronized()|同步|  
|System.Console.Beep()|UI|  
|System.Console.get_Error()|UI|  
|System.Console.get_In()|UI|  
|System.Console.get_KeyAvailable()|UI|  
|System.Console.get_Out()|UI|  
|System.Console.OpenStandardError()|UI|  
|System.Console.OpenStandardInput()|UI|  
|System.Console.OpenStandardOutput()|UI|  
|System.Console.Read()|UI|  
|System.Console.ReadKey()|UI|  
|System.Console.ReadLine()|UI|  
|System.Console.SetError()|UI|  
|System.Console.SetIn()|UI|  
|System.Console.SetOut()|UI|  
|System.Console.Write()|UI|  
|System.Console.WriteLine()|UI|  
|System.Diagnostics.LogMessageEventHandler|ExternalThreading，Synchronization|  
|System.IO.FileStream.BeginRead()|ExternalThreading|  
|System.IO.FileStream.BeginWrite()|ExternalThreading|  
|System.IO.Stream.Synchronized()|同步|  
|System.IO.TextReader.Synchronized()|同步|  
|System.IO.TextWriter.Synchronized()|同步|  
|System.Reflection.Emit.AssemblyBuilder|MayLeakOnAbort|  
|System.Reflection.Emit.ConstructorBuilder|MayLeakOnAbort|  
|System.Reflection.Emit.CustomAttributeBuilder|MayLeakOnAbort|  
|System.Reflection.Emit.EnumBuilder|MayLeakOnAbort|  
|System.Reflection.Emit.EventBuilder|MayLeakOnAbort|  
|System.Reflection.Emit.FieldBuilder|MayLeakOnAbort|  
|System.Reflection.Emit.MethodBuilder|MayLeakOnAbort|  
|System.Reflection.Emit.MethodRental|MayLeakOnAbort|  
|System.Reflection.Emit.ModuleBuilder|MayLeakOnAbort|  
|System.Reflection.Emit.PropertyBuilder|MayLeakOnAbort|  
|System.Reflection.Emit.TypeBuilder|MayLeakOnAbort|  
|System.Reflection.Emit.UnmanagedMarshal|MayLeakOnAbort|  
|System.Security.Principal.WindowsPrincipal|SecurityInfrastructure|  
|System.Threading.AutoResetEvent|ExternalThreading，Synchronization|  
|System.Threading.EventWaitHandle|ExternalThreading，Synchronization|  
|System.Threading.ManualResetEvent|ExternalThreading，Synchronization|  
|System.Threading.Monitor|ExternalThreading，Synchronization|  
|System.Threading.Mutex|ExternalThreading，Synchronization|  
|System.Threading.ReaderWriterLock|ExternalThreading，Synchronization|  
|System.Threading.Thread.AllocateDataSlot()|ExternalThreading，SharedState|  
|System.Threading.Thread.AllocateNamedDataSlot()|ExternalThreading，SharedState|  
|System.Threading.Thread.BeginCriticalRegion()|ExternalThreading，Synchronization|  
|System.Threading.Thread.EndCriticalRegion()|ExternalThreading，Synchronization|  
|System.Threading.Thread.FreeNamedDataSlot()|ExternalThreading，SharedState|  
|System.Threading.Thread.GetData()|ExternalThreading，SharedState|  
|System.Threading.Thread.GetNamedDataSlot()|ExternalThreading，SharedState|  
|System.Threading.Thread.Join()|ExternalThreading，Synchronization|  
|System.Threading.Thread.set_ApartmentState()|Synchronization，SelfAffectingThreading|  
|System.Threading.Thread.set_CurrentUICulture()|ExternalThreading|  
|System.Threading.Thread.set_IsBackground()|SelfAffectingThreading|  
|System.Threading.Thread.set_Name()|ExternalThreading|  
|System.Threading.Thread.set_Priority()|SelfAffectingThreading|  
|System.Threading.Thread.SetApartmentState()|Synchronization，SelfAffectingThreading|  
|System.Threading.Thread.SetData()|ExternalThreading，SharedState|  
|System.Threading.Thread.SpinWait()|ExternalThreading，Synchronization|  
|System.Threading.Thread.Start()|ExternalThreading，Synchronization|  
|System.Threading.Thread.TrySetApartmentState()|Synchronization，SelfAffectingThreading|  
|System.Threading.ThreadPool|ExternalThreading，Synchronization|  
|System.Threading.Timer|ExternalThreading，Synchronization|  
|System.Threading.TimerBase|ExternalThreading，Synchronization|  
  
## <a name="see-also"></a>另请参阅  
 [宿主保护属性和 CLR 集成编程](host-protection-attributes-and-clr-integration-programming.md)   
 [Microsoft.VisualBasic.dll中不允许的类型和成员](disallowed-types-and-members-in-microsoft-visualbasic-dll.md)   
 [System.dll中不允许的类型和成员](disallowed-types-and-members-in-system-dll.md)   
 [System.Data.dll中不允许的类型和成员](disallowed-types-and-members-in-system-data-dll.md)   
 [System.Core.dll 中禁用的类型和成员](disallowed-types-and-members-in-system-core-dll.md)  
  
  
