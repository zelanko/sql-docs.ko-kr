---
title: Reporting Services의 인증 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.topic: reference
helpviewer_keywords:
- security [Reporting Services], authentication
- forms-based authentication [Reporting Services]
- authentication [Reporting Services]
- custom authentication [Reporting Services]
ms.assetid: 103ce1f9-31d8-44bb-b540-2752e4dcf60b
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 2ce82cc9bfb8b3f88934499db4e9295903b67702
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/11/2019
ms.locfileid: "56043204"
---
# <a name="authentication-in-reporting-services"></a>Reporting Services의 인증
  인증은 사용자의 권한을 ID에 설정하는 과정입니다. 사용자를 인증하는 데 사용할 수 있는 많은 방법이 있습니다. 가장 일반적인 방법은 암호를 사용하는 것입니다. 예를 들어 폼 인증을 구현하는 경우 사용자에게 자격 증명을 요구(대개 로그인 이름과 암호를 요구하는 인터페이스를 통해 이루어짐)한 다음 데이터베이스 테이블이나 구성 파일과 같은 데이터 저장소와 대조하여 사용자를 검사하도록 구현합니다. 자격 증명을 확인할 수 없는 경우 인증 프로세스가 실패하고 사용자는 익명 ID를 가집니다.  
  
## <a name="custom-authentication-in-reporting-services"></a>Reporting Services의 사용자 지정 인증  
 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]에서 Windows 운영 체제는 통합 보안을 통해 또는 사용자 자격 증명의 명시적인 수신과 검사를 통해 사용자 인증을 처리합니다. 사용자 지정 인증은 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]에서 개발하여 추가 인증 체계를 지원할 수 있습니다. 보안 확장 프로그램 인터페이스 <xref:Microsoft.ReportingServices.Interfaces.IAuthenticationExtension>을 통해 이 작업을 수행할 수 있습니다. 모든 확장 프로그램은 보고서 서버에서 배포되고 사용되는 모든 확장 프로그램에 대한 <xref:Microsoft.ReportingServices.Interfaces.IExtension> 기본 인터페이스에서 상속됩니다. <xref:Microsoft.ReportingServices.Interfaces.IExtension> 및 <xref:Microsoft.ReportingServices.Interfaces.IAuthenticationExtension>은 <xref:Microsoft.ReportingServices.Interfaces> 네임스페이스의 멤버입니다.  
  
 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]에서 보고서 서버와 대조하여 인증하는 기본적인 방법은 <xref:ReportService2010.ReportingService2010.LogonUser%2A> 메서드입니다. Reporting Services 웹 서비스의 이 멤버는 확인을 위해 사용자 자격 증명을 보고서 서버에 전달하는 데 사용할 수 있습니다. 사용자 기본 보안 확장 프로그램 구현 **IAuthenticationExtension.LogonUser** 에 사용자 지정 인증 코드가 포함 되어 있습니다. 폼 인증 예제에서는 제공된 자격 증명 및 데이터베이스의 사용자 지정 사용자 저장소와 대조하여 인증 검사를 수행하는 **LogonUser**가 있습니다. **LogonUser**의 구현 예는 다음과 같습니다.  
  
```  
public bool LogonUser(string userName, string password, string authority)  
{  
   return AuthenticationUtilities.VerifyPassword(userName, password);  
}  
  
```  
  
 다음 예제 함수는 제공된 자격 증명을 확인하는 데 사용됩니다.  
  
```  
  
internal static bool VerifyPassword(string suppliedUserName,  
   string suppliedPassword)  
{   
   bool passwordMatch = false;  
   // Get the salt and pwd from the database based on the user name.  
   // See "How To: Use DPAPI (Machine Store) from ASP.NET," "How To:  
   // Use DPAPI (User Store) from Enterprise Services," and "How To:  
   // Create a DPAPI Library" for more information about how to use  
   // DPAPI to securely store connection strings.  
   SqlConnection conn = new SqlConnection(  
      "Server=localhost;" +   
      "Integrated Security=SSPI;" +  
      "database=UserAccounts");  
   SqlCommand cmd = new SqlCommand("LookupUser", conn);  
   cmd.CommandType = CommandType.StoredProcedure;  
  
   SqlParameter sqlParam = cmd.Parameters.Add("@userName",  
       SqlDbType.VarChar,  
       255);  
   sqlParam.Value = suppliedUserName;  
   try  
   {  
      conn.Open();  
      SqlDataReader reader = cmd.ExecuteReader();  
      reader.Read(); // Advance to the one and only row  
      // Return output parameters from returned data stream  
      string dbPasswordHash = reader.GetString(0);  
      string salt = reader.GetString(1);  
      reader.Close();  
      // Now take the salt and the password entered by the user  
      // and concatenate them together.  
      string passwordAndSalt = String.Concat(suppliedPassword, salt);  
      // Now hash them  
      string hashedPasswordAndSalt =  
         FormsAuthentication.HashPasswordForStoringInConfigFile(  
         passwordAndSalt,  
         "SHA1");  
      // Now verify them. Returns true if they are equal.  
      passwordMatch = hashedPasswordAndSalt.Equals(dbPasswordHash);  
   }  
   catch (Exception ex)  
   {  
       throw new Exception("Exception verifying password. " +  
          ex.Message);  
   }  
   finally  
   {  
       conn.Close();  
   }  
   return passwordMatch;  
}  
```  
  
## <a name="authentication-flow"></a>인증 흐름  
 Reporting Services 웹 서비스는 보고서 관리자 및 보고서 서버에 의한 폼 인증을 사용할 수 있도록 사용자 지정 인증 확장 프로그램을 제공합니다.  
  
 Reporting Services 웹 서비스의 <xref:ReportService2010.ReportingService2010.LogonUser%2A> 메서드는 인증을 위해 자격 증명을 보고서 서버에 제출하는 데 사용됩니다. 웹 서비스에서는 검사된 로그온 요청에 대해 HTTP 헤더를 사용하여 서버에서 클라이언트로 인증 티켓("쿠키"라고 함)을 전달합니다.  
  
 다음 그림은 사용자 지정 인증 확장 프로그램을 사용하도록 구성된 보고서 서버와 함께 배포된 응용 프로그램의 경우 웹 서비스에 사용자를 인증하는 메서드를 나타냅니다.  
  
 ![Reporting Services 보안 인증 흐름](../../media/rosettasecurityextensionauthenticationflow.gif "Reporting Services 보안 인증 흐름")  
  
 그림 2에 나온 대로 인증 프로세스는 다음과 같습니다.  
  
1.  클라이언트 응용 프로그램에서 사용자를 인증하도록 웹 서비스 <xref:ReportService2010.ReportingService2010.LogonUser%2A> 메서드를 호출합니다.  
  
2.  웹 서비스를 호출 하는 <xref:ReportService2010.ReportingService2010.LogonUser%2A> 메서드의 보안 확장 프로그램 구현 하는 클래스, 특히 **IAuthenticationExtension**합니다.  
  
3.  <xref:ReportService2010.ReportingService2010.LogonUser%2A> 구현에서 사용자 저장소 또는 보안 기관에 있는 사용자 이름과 암호를 검사합니다.  
  
4.  인증이 성공하면 웹 서비스에서 쿠키를 만들고 세션을 위해 관리합니다.  
  
5.  웹 서비스는 HTTP 헤더에서 인증 티켓을 호출 응용 프로그램에 반환합니다.  
  
 웹 서비스에서 보안 확장 프로그램을 통해 사용자를 성공적으로 인증하면 이후 요청에 사용되는 쿠키를 생성합니다. 보고서 서버에 보안 기관이 포함되어 있지 않으므로 쿠키는 사용자 지정 보안 기관 내에 계속 유지되지 않을 수 있습니다. 쿠키는 <xref:ReportService2010.ReportingService2010.LogonUser%2A> 웹 서비스 메서드에서 반환되고 이후 웹 서비스 메서드 호출 및 URL 액세스에서 사용됩니다.  
  
> [!NOTE]  
>  전송 중 쿠키의 노출을 피하려면 <xref:ReportService2010.ReportingService2010.LogonUser%2A>에서 반환된 인증 쿠키를 SSL(Secure Sockets Layer) 암호화를 사용하여 안전하게 전송해야 합니다.  
  
 사용자 지정 보안 확장 프로그램이 설치되어 있는 경우 URL 액세스를 통해 보고서 서버에 액세스하면 IIS(인터넷 정보 서비스) 및 [!INCLUDE[vstecasp](../../../includes/vstecasp-md.md)]에서 인증 티켓 전송을 자동으로 관리합니다. SOAP API를 통해 보고서 서버에 액세스하려는 경우에는 프록시 클래스 구현에서 인증 티켓 관리를 추가로 지원해야 합니다. SOAP API를 사용하고 인증 티켓을 관리하는 방법은 "웹 서비스에서 사용자 지정 보안 사용"을 참조하십시오.  
  
## <a name="forms-authentication"></a>폼 인증  
 폼 인증은 인증되지 않은 사용자를 HTML 양식으로 지정하는 [!INCLUDE[vstecasp](../../../includes/vstecasp-md.md)] 인증 유형입니다. 사용자가 자격 증명을 제공하면 인증 티켓이 포함된 쿠키가 발행됩니다. 이후에 요청이 있으면 먼저 쿠키 검사를 통해 사용자가 보고서 서버에서 이미 인증되었는지 여부에 대한 확인이 이루어집니다.  
  
 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]는 Reporting Services API를 통해 사용 가능한 보안 확장성 인터페이스를 사용하여 폼 인증을 지원하도록 확장할 수 있습니다. [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]를 확장하여 폼 인증을 사용할 경우 보고서 서버와의 모든 통신에 대해 SSL(Secure Sockets Layer)을 사용하여 악의적인 사용자가 다른 사용자의 쿠키에 액세스하지 못하도록 해야 합니다. SSL을 사용하면 클라이언트와 보고서 서버 간의 상호 인증이 가능하며 이 두 컴퓨터 간의 통신 내용을 다른 컴퓨터에서 읽지 못하도록 할 수 있습니다. SSL 연결을 통해 클라이언트에서 전송되는 모든 데이터는 암호화되므로 악의적인 사용자가 보고서 서버로 전송된 암호나 데이터를 가로챌 수 없습니다.  
  
 폼 인증은 일반적으로 Windows 이외의 플랫폼에 대한 계정 및 인증을 지원하기 위해 구현됩니다. 보고서 서버 액세스를 요청하는 사용자는 그래픽 인터페이스를 볼 수 있으며, 제공된 자격 증명은 인증을 위해 보안 기관에 제출됩니다.  
  
 폼 인증에서는 사람이 직접 자격 증명을 입력해야 합니다. Reporting Services 웹 서비스와 직접 통신하는 무인 응용 프로그램의 경우 폼 인증에 사용자 지정 인증 체계를 함께 사용해야 합니다.  
  
 폼 인증은 다음의 경우 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]에 적합합니다.  
  
-   [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows 계정이 없는 사용자를 저장하고 인증해야 하는 경우 및  
  
-   웹 사이트의 다양한 페이지 사이에서 고유의 사용자 인터페이스 양식을 로그온 페이지로 제공해야 하는 경우  
  
 폼 인증을 지원하는 사용자 지정 보안 확장 프로그램을 작성할 때 다음을 고려하십시오.  
  
-   폼 인증을 사용하는 경우 IIS(인터넷 정보 서비스)에서 보고서 서버 가상 디렉터리에 대해 익명 액세스를 사용하도록 설정해야 합니다.  
  
-   [!INCLUDE[vstecasp](../../../includes/vstecasp-md.md)] 인증은 폼 인증으로 설정해야 합니다. 보고서 서버의 경우 Web.config 파일에서 [!INCLUDE[vstecasp](../../../includes/vstecasp-md.md)] 인증을 구성합니다.  
  
-   [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]는 Windows 인증 또는 사용자 지정 인증으로 사용자를 인증하고 권한을 부여할 수 있으며, 두 가지 인증을 모두 사용할 수는 없습니다. [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]에서는 여러 보안 확장 프로그램을 동시에 사용할 수 없습니다.  
  
## <a name="see-also"></a>관련 항목  
 [보안 확장 프로그램 구현](../security-extension/implementing-a-security-extension.md)  
  
  
