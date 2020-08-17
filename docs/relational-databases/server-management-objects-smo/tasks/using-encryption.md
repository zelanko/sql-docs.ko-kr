---
description: 암호화 사용
title: 암호화 사용 | Microsoft Docs
ms.custom: ''
ms.date: 08/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
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
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: d3b777922998a4ef8159f0b2e61a2748d0185a53
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88325363"
---
# <a name="using-encryption"></a>암호화 사용
[!INCLUDE [SQL Server ASDB, ASDBMI, ASDW ](../../../includes/applies-to-version/sql-asdb-asdbmi-asa.md)]

  SMO에서 서비스 마스터 키는 <xref:Microsoft.SqlServer.Management.Smo.ServiceMasterKey> 개체로 표시됩니다. <xref:Microsoft.SqlServer.Management.Smo.Server.ServiceMasterKey%2A> 개체의 <xref:Microsoft.SqlServer.Management.Smo.Server> 속성에서 참조하며, <xref:Microsoft.SqlServer.Management.Smo.ServiceMasterKey.Regenerate%2A> 메서드를 사용하여 다시 생성할 수 있습니다.  
  
 데이터베이스 마스터 키는 <xref:Microsoft.SqlServer.Management.Smo.MasterKey> 개체로 표시됩니다. <xref:Microsoft.SqlServer.Management.Smo.MasterKey.IsEncryptedByServer%2A> 속성은 데이터베이스 마스터 키가 서비스 마스터 키로 암호화되는지 여부를 나타냅니다. 데이터베이스 마스터 키가 변경될 때마다 master 데이터베이스의 암호화된 복사본이 자동으로 업데이트됩니다.  
  
 <xref:Microsoft.SqlServer.Management.Smo.MasterKey.DropServiceKeyEncryption%2A> 메서드를 사용하여 서비스 키 암호화를 삭제하고 암호를 사용하여 데이터베이스 암호화 키를 암호화할 수 있습니다. 이 경우 보안 구성된 프라이빗 키에 액세스하기 전에 데이터베이스 마스터 키를 명시적으로 열어야 합니다.  
  
 데이터베이스가 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스에 연결되어 있으면 데이터베이스 마스터 키에 대한 암호를 제공하거나 <xref:Microsoft.SqlServer.Management.Smo.MasterKey.AddServiceKeyEncryption%2A> 메서드를 실행하여 서비스 마스터 키와 함께 암호화에 사용되는 데이터베이스 마스터 키의 암호화되지 않은 복사본을 만들어야 합니다. 데이터베이스 마스터 키를 명시적으로 열어야 하는 상황을 피하려면 이 단계를 수행하는 것이 좋습니다.  
  
 <xref:Microsoft.SqlServer.Management.Smo.MasterKey.Regenerate%2A> 메서드는 데이터베이스 마스터 키를 다시 생성합니다. 데이터베이스 마스터 키가 다시 생성되면 데이터베이스 마스터 키로 암호화되었던 모든 키가 해독되고 이들을 새 데이터베이스 마스터 키로 암호화합니다. <xref:Microsoft.SqlServer.Management.Smo.MasterKey.DropServiceKeyEncryption%2A> 메서드는 서비스 마스터 키에 의한 데이터베이스 마스터 키의 암호화를 제거합니다. <xref:Microsoft.SqlServer.Management.Smo.MasterKey.AddServiceKeyEncryption%2A>은 마스터 키의 복사본이 서비스 마스터 키를 사용하여 암호화되도록 하고 현재 데이터베이스와 master 데이터베이스에 모두 저장합니다.  
  
 SMO에서 인증서는 <xref:Microsoft.SqlServer.Management.Smo.Certificate> 개체로 표시됩니다. <xref:Microsoft.SqlServer.Management.Smo.Certificate> 개체에는 공개 키, 주체 이름, 유효 기간 및 발급자 정보를 지정하는 속성이 있습니다. 인증서에 대한 액세스 권한은 **Grant**, **Revoke** 및 **Deny** 메서드를 사용하여 제어합니다.  
  
## <a name="example"></a>예제  
 다음 코드 예제를 사용하려면 애플리케이션을 만들 프로그래밍 환경, 프로그래밍 템플릿 및 프로그래밍 언어를 선택해야 합니다. 자세한 내용은 [Visual Studio .net에서 Visual C&#35; SMO 프로젝트 만들기](../../../relational-databases/server-management-objects-smo/how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md)를 참조 하세요.  
  
## <a name="adding-a-certificate-in-visual-c"></a>Visual C#에서 인증서 추가  
 코드 예제는 암호화된 암호를 사용하여 간단한 인증서를 만듭니다. 다른 개체와 달리 <xref:Microsoft.SqlServer.Management.Smo.Certificate.Create%2A> 메서드에는 몇 가지 오버로드가 있습니다. 이 예에 사용된 오버로드는 암호화된 암호를 사용하여 새 인증서를 만듭니다.  
  
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
 코드 예제는 암호화된 암호를 사용하여 간단한 인증서를 만듭니다. 다른 개체와 달리 <xref:Microsoft.SqlServer.Management.Smo.Certificate.Create%2A> 메서드에는 몇 가지 오버로드가 있습니다. 이 예에 사용된 오버로드는 암호화된 암호를 사용하여 새 인증서를 만듭니다.  
  
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
  
## <a name="see-also"></a>참고 항목  
 [암호화 키 사용](../../../relational-databases/server-management-objects-smo/tasks/using-encryption.md)  
  
  
