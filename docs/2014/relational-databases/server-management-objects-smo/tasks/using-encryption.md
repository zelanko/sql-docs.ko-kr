---
title: 암호화를 사용 하 여 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- database master key [SMO]
- cryptography [SMO]
- cryptography [SQL Server], SMO
- encryption keys [SMO]
- encryption [SQL Server], SMO
- encryption [SMO]
- certificates [SMO]
- service master key [SMO]
ms.assetid: 405e0ed7-50a9-430e-a343-471f54b4af76
caps.latest.revision: 25
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: a0d99702b9b6a48e02fe5acc36abed823718c560
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37236733"
---
# <a name="using-encryption"></a>암호화 사용
  SMO에서 서비스 마스터 키로 표현 됩니다는 <xref:Microsoft.SqlServer.Management.Smo.ServiceMasterKey> 개체입니다. 참조 하는이 <xref:Microsoft.SqlServer.Management.Smo.Server.ServiceMasterKey%2A> 의 속성을 <xref:Microsoft.SqlServer.Management.Smo.Server> 개체입니다. 사용 하 여 다시 생성할 수 있습니다는 <xref:Microsoft.SqlServer.Management.Smo.ServiceMasterKey.Regenerate%2A> 메서드.  
  
 데이터베이스 마스터 키가 나타내는 <xref:Microsoft.SqlServer.Management.Smo.MasterKey> 개체입니다. <xref:Microsoft.SqlServer.Management.Smo.MasterKey.IsEncryptedByServer%2A> 속성 데이터베이스 마스터 키가 서비스 마스터 키로 암호화 여부를 나타냅니다. 데이터베이스 마스터 키가 변경될 때마다 master 데이터베이스의 암호화된 복사본이 자동으로 업데이트됩니다.  
  
 서비스 키 암호화를 사용 하 여 삭제할 수 있기를 <xref:Microsoft.SqlServer.Management.Smo.MasterKey.DropServiceKeyEncryption%2A> 메서드 및 암호를 사용 하 여 데이터베이스 마스터 키를 암호화 합니다. 이 경우 보안 구성된 개인 키에 액세스하기 전에 데이터베이스 마스터 키를 명시적으로 열어야 합니다.  
  
 데이터베이스 인스턴스에 연결 중인 경우 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], 데이터베이스 마스터 키에 대 한 암호를 입력 하거나 실행을 <xref:Microsoft.SqlServer.Management.Smo.MasterKey.AddServiceKeyEncryption%2A> 데이터베이스 마스터 키의 암호화 되지 않은 복사본을 사용 가능 서비스를 사용 하 여 암호화 하는 방법 마스터 키입니다. 데이터베이스 마스터 키를 명시적으로 열어야 하는 상황을 피하려면 이 단계를 수행하는 것이 좋습니다.  
  
 <xref:Microsoft.SqlServer.Management.Smo.MasterKey.Regenerate%2A> 메서드는 데이터베이스 마스터 키를 다시 생성 합니다. 데이터베이스 마스터 키가 다시 생성되면 데이터베이스 마스터 키로 암호화되었던 모든 키가 해독되고 이들을 새 데이터베이스 마스터 키로 암호화합니다. <xref:Microsoft.SqlServer.Management.Smo.MasterKey.DropServiceKeyEncryption%2A> 메서드 서비스 마스터 키로 데이터베이스 마스터 키의 암호화를 제거 합니다. <xref:Microsoft.SqlServer.Management.Smo.MasterKey.AddServiceKeyEncryption%2A>은 마스터 키의 복사본이 서비스 마스터 키를 사용하여 암호화되도록 하고 현재 데이터베이스와 master 데이터베이스에 모두 저장합니다.  
  
 SMO에서 인증서는 표시 된 <xref:Microsoft.SqlServer.Management.Smo.Certificate> 개체입니다. <xref:Microsoft.SqlServer.Management.Smo.Certificate> 개체의 공개 키, 주체 이름, 발급자에 대 한 정보와, 유효 기간을 지정 하는 속성입니다. 인증서에 액세스할 수 있는 권한을 사용 하 여 제어 합니다 `Grant`, `Revoke` 및 `Deny` 메서드.  
  
## <a name="example"></a>예제  
 다음 코드 예제를 사용하려면 응용 프로그램을 만들 프로그래밍 환경, 프로그래밍 템플릿 및 프로그래밍 언어를 선택해야 합니다. 자세한 내용은 [Visual Studio.NET에서 Visual Basic SMO 프로젝트 만들기](../../../database-engine/dev-guide/create-a-visual-basic-smo-project-in-visual-studio-net.md) 및 [Visual C 만들기&#35; Visual Studio.NET에서 SMO 프로젝트](../how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md)합니다.  
  
## <a name="adding-a-certificate-in-visual-basic"></a>Visual Basic에서 인증서 추가  
 코드 예제는 암호화된 암호를 사용하여 간단한 인증서를 만듭니다. 다른 개체와 달리는 <xref:Microsoft.SqlServer.Management.Smo.Certificate.Create%2A> 메서드에 몇 가지 오버 로드가 있습니다. 이 예에 사용된 오버로드는 암호화된 암호를 사용하여 새 인증서를 만듭니다.  
  
<!-- TODO: review snippet reference  [!CODE [SMO How to#SMO_VBCertificate1](SMO How to#SMO_VBCertificate1)]  -->  
  
## <a name="adding-a-certificate-in-visual-c"></a>Visual C#에서 인증서 추가  
 코드 예제는 암호화된 암호를 사용하여 간단한 인증서를 만듭니다. 다른 개체와 달리는 <xref:Microsoft.SqlServer.Management.Smo.Certificate.Create%2A> 메서드에 몇 가지 오버 로드가 있습니다. 이 예에 사용된 오버로드는 암호화된 암호를 사용하여 새 인증서를 만듭니다.  
  
```  
{  
            //Connect to the local, default instance of SQL Server.   
            {  
                Server srv = new Server();  
  
                //Reference the AdventureWorks2012 database.   
                Database db = srv.Databases["AdventureWorks2012"];  
  
                //Define a Certificate object variable by supplying the parent database and name in the constructor.   
                Certificate c = new Certificate(db, "Test_Certificate");  
  
                //Set the start date, expiry date, and description.   
                System.DateTime dt;  
                DateTime.TryParse("January 01, 2010", out dt);  
                c.StartDate = dt;  
                DateTime.TryParse("January 01, 2015", out dt);  
                c.ExpirationDate = dt;  
                c.Subject = "This is a test certificate.";  
                //Create the certificate on the instance of SQL Server by supplying the certificate password argument.   
                c.Create("pGFD4bb925DGvbd2439587y");  
            }  
        }   
```  
  
## <a name="adding-a-certificate-in-powershell"></a>PowerShell에서 인증서 추가  
 코드 예제는 암호화된 암호를 사용하여 간단한 인증서를 만듭니다. 다른 개체와 달리는 <xref:Microsoft.SqlServer.Management.Smo.Certificate.Create%2A> 메서드에 몇 가지 오버 로드가 있습니다. 이 예에 사용된 오버로드는 암호화된 암호를 사용하여 새 인증서를 만듭니다.  
  
```  
# Set the path context to the local, default instance of SQL Server and get a reference to AdventureWorks2012  
CD \sql\localhost\default\databases  
$db = get-item AdventureWorks2012  
  
#Create a certificate  
  
$c = New-Object -TypeName Microsoft.SqlServer.Management.Smo.Certificate -argumentlist $db, "Test_Certificate"  
$c.StartDate = "January 01, 2010"  
$c.Subject = "This is a test certificate."  
$c.ExpirationDate = "January 01, 2015"  
  
#Create the certificate on the instance of SQL Server by supplying the certificate password argument.  
$c.Create("pGFD4bb925DGvbd2439587y")  
  
```  
  
## <a name="see-also"></a>관련 항목  
 [암호화 키를 사용 하 여](using-encryption.md)  
  
  
