---
title: URL 액세스를 사용 하 여 보고서 서버 항목 액세스 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- referencing URL items for report server access
- URL access [Reporting Services], report servers
ms.assetid: a58b4ca6-129d-45e9-95c7-e9169fe5bba4
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 3a345cd609c4cfd79f9e93a2b63e71bbddde36ee
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63233564"
---
# <a name="access-report-server-items-using-url-access"></a>URL 액세스를 사용 하 여 보고서 서버 항목 액세스
  이 항목에서는 설명 하는 방법을 보고서에서 여러 형식의 카탈로그 항목에 액세스 하려면 서버 데이터베이스 또는 SharePoint 사이트를 사용 하 여 *rs: Command*=*값*합니다.  
  
 이 매개 변수 문자열을 추가할 필요는 없습니다. 를 생략 하면 보고서 서버에서 항목 형식을 평가 하 고 적절 한 매개 변수 값을 자동으로 선택 합니다. 그러나 사용 하는 *rs: Command*=*값* URL의 문자열에는 보고서 서버 성능을 향상 시킵니다.  
  
 참고는 `_vti_bin` 아래 예제에서는 프록시 구문입니다. 프록시 구문을 사용 하는 방법에 대 한 자세한 내용은 참조 하세요. [URL Access Parameter Reference](url-access-parameter-reference.md)합니다.  
  
## <a name="access-a-report"></a>보고서에 액세스  
 브라우저에서 보고서를 보려면를 사용 합니다 *rs: Command*=*렌더링* 매개 변수입니다. 예를 들어:  
  
 `Native` `http://myrshost/reportserver?/Sales/YearlySalesByCategory&rs:Command=Render`  
  
 `SharePoint` `http://myspsite/subsite/_vti_bin/reportserver? http://myspsite/subsite/Sales/YearlySalesByCategory&rs:Command=Render`  
  
> [!TIP]  
>  URL에는 SharePoint를 통해 요청을 라우팅하는 `_vti_bin` 프록시 구문과 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] HTTP 프록시를 포함하는 것이 중요합니다. 프록시는 몇 가지 컨텍스트를 HTTP 요청에 추가하며 이 컨텍스트는 SharePoint 모드 보고서 서버에 대한 보고서의 올바른 실행을 보장하는 데 필요합니다.  
  
## <a name="access-a-resource"></a>리소스에 액세스  
 리소스에 액세스 하려면 사용 합니다 *rs: Command*=*GetResourceContents* 매개 변수입니다. 리소스 이미지와 같이 브라우저와 호환 되 면 브라우저에서 열립니다. 그렇지 않으면 파일 또는 리소스를 열거나 디스크에 저장하라는 메시지가 나타납니다.  
  
 `Native` `http://myrshost/reportserver?/Sales/StorePicture&rs:Command=GetResourceContents`  
  
 `SharePoint` `http://myspsite/subsite/_vti_bin/reportserver? http://myspsite/subsite/Sales/StorePicture.jpg&rs:Command=GetResourceContents`  
  
## <a name="access-a-data-source"></a>데이터 원본에 액세스  
 데이터 원본에 액세스 하려면 사용 합니다 *rs: Command*=*GetDataSourceContents* 매개 변수입니다. 인증된 된 사용자가 있다면 데이터 원본 정의가 표시 됩니다 브라우저에서 XML을 지 원하는 경우 `Read Contents` 데이터 원본에 대 한 권한이 있습니다. 예를 들어:  
  
 `Native` `http://myrshost/reportserver?/Sales/AdventureWorks2012&rs:Command=GetDataSourceContents`  
  
 `SharePoint` `http://myspsite/subsite/_vti_bin/reportserver? http://myspsite/subsite/Sales/AdventureWorks2012&rs:Command=GetDataSourceContents`  
  
 XML 구조는 다음 예와 같습니다.  
  
```  
<DataSourceDefinition>  
   <Extension>SQL</Extension>  
   <ConnectString>Provider=SQLOLEDB.1;Integrated Security=SSPI;Persist Security Info=False;Initial Catalog=AdventureWorks2012;Data Source=MYSERVER1;</ConnectString>  
   <CredentialRetrieval>Integrated</CredentialRetrieval>  
   <WindowsCredentials>False</WindowsCredentials>  
   <ImpersonateUser>False</ImpersonateUser>  
   <Prompt />  
   <Enabled>True</Enabled>  
</DataSourceDefinition>  
```  
  
 연결 문자열에 따라 반환 되는 **SecureConnectionLevel** 보고서 서버를 설정 합니다. 에 대 한 자세한 내용은 합니다 **SecureConnectionLevel** 설정을 참조 하세요 [Using Secure Web Service Methods](report-server-web-service/net-framework/using-secure-web-service-methods.md)합니다.  
  
## <a name="access-the-contents-of-a-folder"></a>폴더의 내용에 액세스  
 폴더의 내용에 액세스 하려면 사용 합니다 *rs: Command*=*GetChildren* 매개 변수입니다. 일반적인 폴더 탐색 페이지가 하위 폴더, 보고서, 데이터 원본 및 요청된 된 폴더의 리소스에 대 한 링크를 포함 하는 반환 됩니다. 예를 들어:  
  
 `Native` `http://myrshost/reportserver?/Sales&rs:Command=GetChildren`  
  
 `SharePoint` `http://myspsite/subsite/_vti_bin/reportserver? http://myspsite/subsite/Sales&rs:Command=GetChildren`  
  
 디렉터리 검색 사용 되는 모드 사용자 인터페이스 표시 비슷합니다 [!INCLUDE[msCoName](../includes/msconame-md.md)] 인터넷 정보 서버 (IIS). 보고서 서버의 빌드 번호를 포함 하 여 버전 번호를 아래 폴더 목록도 표시 됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [URL 액세스 &#40;SSRS&#41;](url-access-ssrs.md)   
 [URL 액세스 매개 변수 참조](url-access-parameter-reference.md)  
  
  
