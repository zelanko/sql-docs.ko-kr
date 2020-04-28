---
title: System.object에서 허용 되지 않는 형식 및 멤버 | Microsoft Docs
description: SQL Server CLR 프로그래밍에서는 HostProtectionResource 열거형의 일부 값을 가진 형식 또는 멤버를 허용 하지 않습니다. 이 문서에서는 System.object를 사용할 때 허용 되지 않는 값을 나열 합니다.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
ms.assetid: dcd24cd6-f4ab-42cc-9786-a1604e8a4b4e
author: rothja
ms.author: jroth
ms.openlocfilehash: e89af3c6f93fb6c8576a6e627eed8e984fb0f0ae
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81486871"
---
# <a name="disallowed-types-and-members-in-systemcoredll"></a>System.Core.dll에 허용되지 않는 유형 및 멤버
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]CLR (공용 언어 통합) 프로그래밍에서는 **Externalprocessmgmt**, **externalprocessor**, **MayLeakOnAbort**, **securityinfrastructure**, **SelfAffectingProcessMgmnt**, **SelfAffectingThreading**, **sharedstate**, **Synchronization**또는 **UI**값을 사용 하 여 **HostProtectionResource** 열거형을 지정 하는 **HostProtectionAttribute** 을 포함 하는 형식 또는 멤버를 사용할 때를 허용 하지 않습니다. 다음 표에는 HPA(호스트 보호 특성) 값이 허용되지 않는 System.Core.dll 어셈블리의 멤버 및 유형이 나열되어 있습니다.  
  
> [!NOTE]  
>  이 목록은 지원되는 어셈블리에서 생성되었습니다. 자세한 내용은 [Supported .NET Framework Libraries](../../relational-databases/clr-integration/database-objects/supported-net-framework-libraries.md)을 참조하세요.  
  
|유형 또는 멤버|HPA 값|  
|--------------------|--------------------|  
|System.Diagnostics.Eventing.EventDescriptor|MayLeakOnAbort|  
|System.Diagnostics.Eventing.EventProvider|MayLeakOnAbort|  
|System.Diagnostics.Eventing.EventProviderTraceListener|MayLeakOnAbort|  
|System.Management.Instrumentation.ManagementEntityAttribute|MayLeakOnAbort|  
|System.Management.Instrumentation.WmiConfigurationAttribute|MayLeakOnAbort|  
|System.Management.Instrumentation.ManagementMemberAttribute|MayLeakOnAbort|  
|System.Management.Instrumentation.ManagementNewInstanceAttribute|MayLeakOnAbort|  
|System.Management.Instrumentation.ManagementBindAttribute|MayLeakOnAbort|  
|System.Management.Instrumentation.ManagementCreateAttribute|MayLeakOnAbort|  
|System.Management.Instrumentation.ManagementRemoveAttribute|MayLeakOnAbort|  
|System.Management.Instrumentation.ManagementEnumeratorAttribute|MayLeakOnAbort|  
|System.Management.Instrumentation.ManagementProbeAttribute|MayLeakOnAbort|  
|System.Management.Instrumentation.ManagementTaskAttribute|MayLeakOnAbort|  
|System.Management.Instrumentation.ManagementKeyAttribute|MayLeakOnAbort|  
|System.Management.Instrumentation.ManagementReferenceAttribute|MayLeakOnAbort|  
|System.Management.Instrumentation.ManagementConfigurationAttribute|MayLeakOnAbort|  
|System.Management.Instrumentation.ManagementCommitAttribute|MayLeakOnAbort|  
|System.Management.Instrumentation.ManagementNameAttribute|MayLeakOnAbort|  
|System.Management.Instrumentation.InstrumentationBaseException|MayLeakOnAbort|  
|System.Management.Instrumentation.InstrumentationException|MayLeakOnAbort|  
|System.Management.Instrumentation.InstanceNotFoundException|MayLeakOnAbort|  
|System.Diagnostics.Eventing.Reader.EventBookmark|MayLeakOnAbort|  
|System.Diagnostics.Eventing.Reader.EventLogConfiguration|MayLeakOnAbort|  
|System.Diagnostics.Eventing.Reader.EventLogLink|MayLeakOnAbort|  
|System.Diagnostics.Eventing.Reader.EventLogStatus|MayLeakOnAbort|  
|System.Diagnostics.Eventing.Reader.EventProperty|MayLeakOnAbort|  
|System.Diagnostics.Eventing.Reader.EventLogPropertySelector|MayLeakOnAbort|  
|System.Diagnostics.Eventing.Reader.EventRecord|MayLeakOnAbort|  
|System.Diagnostics.Eventing.Reader.EventKeyword|MayLeakOnAbort|  
|System.Diagnostics.Eventing.Reader.EventLevel|MayLeakOnAbort|  
|System.Diagnostics.Eventing.Reader.EventLogRecord|MayLeakOnAbort|  
|System.Diagnostics.Eventing.Reader.EventLogReader|MayLeakOnAbort|  
|System.Diagnostics.Eventing.Reader.EventLogWatcher|MayLeakOnAbort|  
|System.Diagnostics.Eventing.Reader.EventRecordWrittenEventArgs|MayLeakOnAbort|  
|System.Diagnostics.Eventing.Reader.EventLogSession|MayLeakOnAbort|  
|System.Diagnostics.Eventing.Reader.EventMetadata|MayLeakOnAbort|  
|System.Diagnostics.Eventing.Reader.EventOpcode|MayLeakOnAbort|  
|System.Diagnostics.Eventing.Reader.EventTask|MayLeakOnAbort|  
|System.Diagnostics.Eventing.Reader.EventLogException|MayLeakOnAbort|  
|System.Diagnostics.Eventing.Reader.EventLogNotFoundException|MayLeakOnAbort|  
|System.Diagnostics.Eventing.Reader.EventLogReadingException|MayLeakOnAbort|  
|System.Diagnostics.Eventing.Reader.EventLogProviderDisabledException|MayLeakOnAbort|  
|System.Diagnostics.Eventing.Reader.EventLogInvalidDataException|MayLeakOnAbort|  
|System.Diagnostics.Eventing.Reader.EventLogInformation|MayLeakOnAbort|  
|System.Diagnostics.Eventing.Reader.ProviderMetadata|MayLeakOnAbort|  
|Microsoft.Win32.SafeHandles.SafeNCryptHandle|MayLeakOnAbort|  
|Microsoft.Win32.SafeHandles.SafeNCryptKeyHandle|MayLeakOnAbort|  
|Microsoft.Win32.SafeHandles.SafeNCryptProviderHandle|MayLeakOnAbort|  
|Microsoft.Win32.SafeHandles.SafeNCryptSecretHandle|MayLeakOnAbort|  
|System.Security.Cryptography.Aes|MayLeakOnAbort|  
|System.Security.Cryptography.AesCryptoServiceProvider|MayLeakOnAbort|  
|System.Security.Cryptography.AesManaged|MayLeakOnAbort|  
|System.Security.Cryptography.CngAlgorithm|MayLeakOnAbort|  
|System.Security.Cryptography.CngAlgorithmGroup|MayLeakOnAbort|  
|System.Security.Cryptography.CngKey|MayLeakOnAbort|  
|System.Security.Cryptography.CngKeyBlobFormat|MayLeakOnAbort|  
|System.Security.Cryptography.CngKeyCreationParameters|MayLeakOnAbort|  
|System.Security.Cryptography.CngProperty|MayLeakOnAbort|  
|System.Security.Cryptography.CngPropertyCollection|MayLeakOnAbort|  
|System.Security.Cryptography.CngProvider|MayLeakOnAbort|  
|System.Security.Cryptography.CngUIPolicy|MayLeakOnAbort|  
|System.Security.Cryptography.ECDiffieHellman|MayLeakOnAbort|  
|System.Security.Cryptography.ECDiffieHellmanPublicKey|MayLeakOnAbort|  
|System.Security.Cryptography.ECDiffieHellmanCng|MayLeakOnAbort|  
|System.Security.Cryptography.ECDiffieHellmanCngPublicKey|MayLeakOnAbort|  
|System.Security.Cryptography.ECDsa|MayLeakOnAbort|  
|System.Security.Cryptography.ECDsaCng|MayLeakOnAbort|  
|System.Security.Cryptography.ManifestSignatureInformation|MayLeakOnAbort|  
|System.Security.Cryptography.ManifestSignatureInformationCollection|MayLeakOnAbort|  
|System.Security.Cryptography.MD5Cng|MayLeakOnAbort|  
|System.Security.Cryptography.SHA1Cng|MayLeakOnAbort|  
|System.Security.Cryptography.SHA256Cng|MayLeakOnAbort|  
|System.Security.Cryptography.SHA256CryptoServiceProvider|MayLeakOnAbort|  
|System.Security.Cryptography.SHA384Cng|MayLeakOnAbort|  
|System.Security.Cryptography.SHA384CryptoServiceProvider|MayLeakOnAbort|  
|System.Security.Cryptography.SHA512Cng|MayLeakOnAbort|  
|System.Security.Cryptography.SHA512CryptoServiceProvider|MayLeakOnAbort|  
|System.Security.Cryptography.StrongNameSignatureInformation|MayLeakOnAbort|  
|System.Security.Cryptography.X509Certificates.AuthenticodeSignatureInformation|MayLeakOnAbort|  
|System.Security.Cryptography.X509Certificates.TimestampInformation|MayLeakOnAbort|  
|Microsoft.Win32.SafeHandles.SafePipeHandle|MayLeakOnAbort|  
|System.TimeZoneInfo|MayLeakOnAbort|  
|System.TimeZoneNotFoundException|MayLeakOnAbort|  
|System.InvalidTimeZoneException|MayLeakOnAbort|  
|System.Diagnostics.EventSchemaTraceListener|MayLeakOnAbort|  
|System.Diagnostics.UnescapedXmlDiagnosticData|MayLeakOnAbort|  
|System.Diagnostics.PerformanceData.CounterData|MayLeakOnAbort|  
|System.Diagnostics.PerformanceData.CounterSetInstanceCounterDataSet|MayLeakOnAbort|  
|System.Diagnostics.PerformanceData.CounterSet|MayLeakOnAbort|  
|System.Diagnostics.PerformanceData.CounterSetInstance|MayLeakOnAbort|  
|System.Collections.Generic.HashSet`1|MayLeakOnAbort|  
|System.IO.Pipes.PipeStream|MayLeakOnAbort|  
|System.IO.Pipes.AnonymousPipeServerStream|MayLeakOnAbort|  
|System.IO.Pipes.AnonymousPipeClientStream|MayLeakOnAbort|  
|System.IO.Pipes.NamedPipeServerStream|MayLeakOnAbort|  
|System.IO.Pipes.NamedPipeClientStream|MayLeakOnAbort|  
|System.IO.Pipes.PipeAccessRule|MayLeakOnAbort|  
|System.IO.Pipes.PipeAuditRule|MayLeakOnAbort|  
|System.IO.Pipes.PipeSecurity|MayLeakOnAbort|  
|System.Threading.LockRecursionException|MayLeakOnAbort|  
|System.Threading.ReaderWriterLockSlim|MayLeakOnAbort|  
  
## <a name="see-also"></a>참고 항목  
 [호스트 보호 특성 및 CLR 통합 프로그래밍](../../relational-databases/clr-integration-security-host-protection-attributes/host-protection-attributes-and-clr-integration-programming.md)   
 [Microsoft.visualbasic에 허용 되지 않는 형식 및 멤버](../../relational-databases/clr-integration-security-host-protection-attributes/disallowed-types-and-members-in-microsoft-visualbasic-dll.md)   
 [Mscorlib.dll에 허용 되지 않는 형식 및 멤버](../../relational-databases/clr-integration-security-host-protection-attributes/disallowed-types-and-members-in-mscorlib-dll.md)   
 [System.object의 허용 되지 않는 형식 및 멤버](../../relational-databases/clr-integration-security-host-protection-attributes/disallowed-types-and-members-in-system-dll.md)   
 [System.Data.dll에 허용되지 않는 유형 및 멤버](../../relational-databases/clr-integration-security-host-protection-attributes/disallowed-types-and-members-in-system-data-dll.md)  
  
  
