---
title: URL 액세스를 사용하여 보고서 서버 항목 액세스 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- referencing URL items for report server access
- URL access [Reporting Services], report servers
ms.assetid: a58b4ca6-129d-45e9-95c7-e9169fe5bba4
caps.latest.revision: 41
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: e7184a0a5aa72ea7fe4ff681103044f2791bdf33
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37227097"
---
# <a name="access-report-server-items-using-url-access"></a>URL 액세스를 사용하여 보고서 서버 항목 액세스
  이 항목에서는 *rs:Command*=*Value*를 사용하여 보고서 서버 데이터베이스 또는 SharePoint 사이트에서 여러 형식의 카탈로그 항목에 액세스하는 방법에 대해 설명합니다.  
  
 이 매개 변수 문자열을  추가할 필요는 없습니다. 이 문자열을 생략한 경우 보고서 서버에서 항목 형식을 평가하고 알맞은 매개 변수 값을 자동으로 선택합니다. 그러나 URL에서 *rs:Command*=*Value* 문자열을 사용하면 보고서 서버의 성능이 향상됩니다.  
  
 아래 예의 `_vti_bin` 프록시 구문을 참고하십시오. 프록시 구문을 사용 하는 방법에 대 한 자세한 내용은 참조 하세요. [URL Access Parameter Reference](url-access-parameter-reference.md)합니다.  
  
## <a name="access-a-report"></a>보고서 액세스  
 브라우저에서 보고서를 보려면 *rs:Command*=*Render* 매개 변수를 사용합니다. 예를 들어:  
  
 `Native` `http://myrshost/reportserver?/Sales/YearlySalesByCategory&rs:Command=Render`  
  
 `SharePoint` `http://myspsite/subsite/_vti_bin/reportserver?http://myspsite/subsite/Sales/YearlySalesByCategory&rs:Command=Render`  
  
> [!TIP]  
>  URL에는 SharePoint를 통해 요청을 라우팅하는 `_vti_bin` 프록시 구문과 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] HTTP 프록시를 포함하는 것이 중요합니다. 프록시는 몇 가지 컨텍스트를 HTTP 요청에 추가하며 이 컨텍스트는 SharePoint 모드 보고서 서버에 대한 보고서의 올바른 실행을 보장하는 데 필요합니다.  
  
## <a name="access-a-resource"></a>리소스 액세스  
 리소스에 액세스하려면 *rs:Command*=*GetResourceContents* 매개 변수를 사용합니다. 이미지와 같이 브라우저와 호환되는 리소스는 브라우저에서 열립니다. 그렇지 않으면 파일 또는 리소스를 열거나 디스크에 저장하라는 메시지가 나타납니다.  
  
 `Native` `http://myrshost/reportserver?/Sales/StorePicture&rs:Command=GetResourceContents`  
  
 `SharePoint` `http://myspsite/subsite/_vti_bin/reportserver?http://myspsite/subsite/Sales/StorePicture.jpg&rs:Command=GetResourceContents`  
  
## <a name="access-a-data-source"></a>데이터 원본 액세스  
 데이터 원본에 액세스하려면 *rs:Command*=*GetDataSourceContents* 매개 변수를 사용합니다. 브라우저에서 XML을 지원하는 경우 데이터 원본에 대해 `Read Contents` 권한을 가진 인증된 사용자이면 데이터 원본 정의가 표시됩니다. 예를 들어:  
  
 `Native` `http://myrshost/reportserver?/Sales/AdventureWorks2012&rs:Command=GetDataSourceContents`  
  
 `SharePoint` `http://myspsite/subsite/_vti_bin/reportserver?http://myspsite/subsite/Sales/AdventureWorks2012&rs:Command=GetDataSourceContents`  
  
 XML 구조는 다음 예와 유사합니다.  
  
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
  
 연결 문자열은 보고서 서버의 **SecureConnectionLevel** 설정을 기준으로 반환됩니다. 에 대 한 자세한 내용은 합니다 **SecureConnectionLevel** 설정을 참조 하세요 [Using Secure Web Service Methods](report-server-web-service/net-framework/using-secure-web-service-methods.md)합니다.  
  
## <a name="access-the-contents-of-a-folder"></a>폴더 내용 액세스  
 폴더의 내용에 액세스하려면 *rs:Command*=*GetChildren* 매개 변수를 사용합니다. 요청된 폴더의 하위 폴더, 보고서, 데이터 원본 및 리소스에 대한 링크가 포함된 일반적인 폴더 탐색 페이지가 반환됩니다. 예를 들어:  
  
 `Native` `http://myrshost/reportserver?/Sales&rs:Command=GetChildren`  
  
 `SharePoint` `http://myspsite/subsite/_vti_bin/reportserver?http://myspsite/subsite/Sales&rs:Command=GetChildren`  
  
 표시되는 사용자 인터페이스는 [!INCLUDE[msCoName](../includes/msconame-md.md)] IIS(Internet Information Server)에서 사용되는 디렉터리 탐색 모드와 유사합니다. 빌드 번호를 포함한 보고서 서버의 버전 번호도 폴더 목록 아래에 표시됩니다.  
  
## <a name="see-also"></a>관련 항목  
 [URL 액세스 &#40;SSRS&#41;](url-access-ssrs.md)   
 [URL 액세스 매개 변수 참조](url-access-parameter-reference.md)  
  
  
