---
title: "암호화를 사용 하 여 | Microsoft Docs"
ms.custom: 
ms.date: 08/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: smo
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
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
caps.latest.revision: "27"
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ad74e5242702ace386fb8c14a034a56886f27191
ms.sourcegitcommit: cb2f9d4db45bef37c04064a9493ac2c1d60f2c22
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/12/2018
---
# <a name="using-encryption"></a>암호화 사용
[!INCLUDE[appliesto-ss-asdb-asdw-xxx-md](../../../includes/appliesto-ss-asdb-asdw-xxx-md.md)]

  SMO에서 서비스 마스터 키로 표현 됩니다는 <xref:Microsoft.SqlServer.Management.Smo.ServiceMasterKey> 개체입니다. 참조는 <xref:Microsoft.SqlServer.Management.Smo.Server.ServiceMasterKey%2A> 의 속성은 <xref:Microsoft.SqlServer.Management.Smo.Server> 개체입니다. 사용 하 여 다시 생성할 수 있습니다는 <xref:Microsoft.SqlServer.Management.Smo.ServiceMasterKey.Regenerate%2A> 메서드.  
  
 데이터베이스 마스터 키가 나타내는 <xref:Microsoft.SqlServer.Management.Smo.MasterKey> 개체입니다. <xref:Microsoft.SqlServer.Management.Smo.MasterKey.IsEncryptedByServer%2A> 속성은 데이터베이스 마스터 키는 서비스 마스터 키로 암호화 되어 있는지 여부를 나타냅니다. 데이터베이스 마스터 키가 변경될 때마다 master 데이터베이스의 암호화된 복사본이 자동으로 업데이트됩니다.  
  
 서비스 키 암호화를 사용 하 여 삭제할 수는 <xref:Microsoft.SqlServer.Management.Smo.MasterKey.DropServiceKeyEncryption%2A> 메서드 암호로 데이터베이스 마스터 키를 암호화 합니다. 이 경우 보안 구성된 개인 키에 액세스하기 전에 데이터베이스 마스터 키를 명시적으로 열어야 합니다.  
  
 데이터베이스 인스턴스에 연결 중인 경우 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], 데이터베이스 마스터 키에 대 한 암호를 제공 하거나 실행 해야 합니다는 <xref:Microsoft.SqlServer.Management.Smo.MasterKey.AddServiceKeyEncryption%2A> 서비스와 함께 암호화에 사용할 수 있는 데이터베이스 마스터 키의 암호화 되지 않은 복사본을 만드는 메서드와 알림이 마스터 키입니다. 데이터베이스 마스터 키를 명시적으로 열어야 하는 상황을 피하려면 이 단계를 수행하는 것이 좋습니다.  
  
 <xref:Microsoft.SqlServer.Management.Smo.MasterKey.Regenerate%2A> 메서드 데이터베이스 마스터 키를 다시 생성 합니다. 데이터베이스 마스터 키가 다시 생성되면 데이터베이스 마스터 키로 암호화되었던 모든 키가 해독되고 이들을 새 데이터베이스 마스터 키로 암호화합니다. <xref:Microsoft.SqlServer.Management.Smo.MasterKey.DropServiceKeyEncryption%2A> 메서드 서비스 마스터 키로 데이터베이스 마스터 키의 암호화를 제거 합니다. <xref:Microsoft.SqlServer.Management.Smo.MasterKey.AddServiceKeyEncryption%2A>은 마스터 키의 복사본이 서비스 마스터 키를 사용하여 암호화되도록 하고 현재 데이터베이스와 master 데이터베이스에 모두 저장합니다.  
  
 SMO에서 인증서도 표시 됩니다는 <xref:Microsoft.SqlServer.Management.Smo.Certificate> 개체입니다. <xref:Microsoft.SqlServer.Management.Smo.Certificate> 개체에 공개 키, 주체 이름, 유효 기간, 및 발급자에 대 한 정보를 지정 하는 속성이 있습니다. 인증서에 대한 액세스 권한은 **Grant**, **Revoke** 및 **Deny** 메서드를 사용하여 제어합니다.  
  
## <a name="example"></a>예제  
 다음 코드 예제를 사용하려면 응용 프로그램을 만들 프로그래밍 환경, 프로그래밍 템플릿 및 프로그래밍 언어를 선택해야 합니다. 자세한 내용은 참조 [만들기 Visual C & #35; Visual Studio.NET에서에서 SMO 프로젝트](../../../relational-databases/server-management-objects-smo/how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md)합니다.  
  
## <a name="adding-a-certificate-in-visual-c"></a>Visual C#에서 인증서 추가  
 코드 예제는 암호화된 암호를 사용하여 간단한 인증서를 만듭니다. 다른 개체와 달리는 <xref:Microsoft.SqlServer.Management.Smo.Certificate.Create%2A> 메서드에 여러 오버 로드가 있습니다. 이 예에 사용된 오버로드는 암호화된 암호를 사용하여 새 인증서를 만듭니다.  
  
```csharp  
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
 코드 예제는 암호화된 암호를 사용하여 간단한 인증서를 만듭니다. 다른 개체와 달리는 <xref:Microsoft.SqlServer.Management.Smo.Certificate.Create%2A> 메서드에 여러 오버 로드가 있습니다. 이 예에 사용된 오버로드는 암호화된 암호를 사용하여 새 인증서를 만듭니다.  
  
```powershell  
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
  
## <a name="see-also"></a>관련 항목:  
 [암호화 키를 사용 하 여](../../../relational-databases/server-management-objects-smo/tasks/using-encryption.md)  
  
  
