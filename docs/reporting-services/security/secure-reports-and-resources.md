---
title: "보고서 및 리소스 보안 | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- security [Reporting Services], reports
- security [Reporting Services], resources
- reports [Reporting Services], security
- confidential reports [Reporting Services]
- resources [Reporting Services], security
ms.assetid: 63cd55c7-fd2a-49e3-a3f8-59eb1a1c6e83
caps.latest.revision: 47
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 66e32b412558ec3c06fcbfcb3b4dbd1b7b2e06e0
ms.contentlocale: ko-kr
ms.lasthandoff: 06/13/2017

---
# <a name="secure-reports-and-resources"></a>보고서 및 리소스 보안
  개별 보고서 및 리소스에 보안을 설정하여 사용자가 해당 항목에 대해 갖는 액세스 수준을 제어할 수 있습니다. 기본적으로 **Administrators** 기본 제공 그룹의 멤버인 사용자만 보고서 실행, 리소스 보기, 속성 수정, 항목 삭제 등의 작업을 수행할 수 있습니다. 다른 모든 사용자는 보고서나 리소스에 대한 액세스를 허용하는 역할 할당이 만들어져 있어야 합니다.  
  
## <a name="role-based-access-to-reports-and-resources"></a>보고서 및 리소스에 대한 역할 기반 액세스  
 보고서 및 리소스에 대한 액세스 권한을 부여하려면 사용자가 부모 폴더에서 기존 역할 할당을 상속할 수 있도록 하거나 항목 자체에 대한 새 역할 할당을 만듭니다.  
  
 대부분의 경우 부모 폴더에서 상속된 권한을 사용하는 것이 좋습니다. 보고서나 리소스의 존재 여부를 알 필요가 없는 사용자가 해당 보고서나 리소스를 볼 수 없도록 하거나 보고서 또는 항목에 대한 액세스 수준을 높이려는 경우에만 개별 보고서와 리소스에 대한 보안을 설정해야 합니다. 이러한 보안 설정 방식은 상호 배타적인 것이 아닙니다. 보다 적은 수의 사용자만 보고서에 액세스할 수 있도록 제한하고 이들 중 일부 또는 모두에게 보고서를 관리할 수 있는 추가 권한을 제공할 수 있습니다.  
  
 이러한 보안 설정을 위해서는 역할 할당을 여러 개 만들 필요가 있습니다. 예를 들어 사용자 이영희, 김철수 및 인사 관리자 그룹만 보고서에 액세스할 수 있도록 설정하는 경우 이영희와 김철수에게는 보고서 관리 권한을, 인사 관리자 그룹 멤버에게는 보고서 실행 권한만 부여하려고 합니다. 이러한 사용자 모두에게 보안을 설정하려면 이영희를 보고서의 내용 관리자로 만드는 역할 할당, 김철수를 보고서의 내용 관리자로 만드는 역할 할당, 인사 관리자 그룹에게 보기 전용 태스크를 지원하는 역할 할당을 만들어야 합니다.  
  
 보고서 또는 리소스에 보안을 설정한 경우 이러한 설정은 항목을 새 위치로 이동하더라도 해당 항목에 그대로 적용됩니다. 예를 들어 일부 사용자에게만 액세스 권한이 부여된 보고서를 이동할 경우 상대적으로 개방된 보안 정책을 갖는 폴더로 보고서를 이동하더라도 해당 사용자들만 보고서를 계속 사용할 수 있습니다.  
  
## <a name="mitigating-html-injection-attacks-in-a-published-report-or-document"></a>게시된 보고서 또는 문서의 HTML 삽입 공격 위험 완화  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]에서 보고서와 리소스는 보고서를 실행 중인 사용자의 보안 ID로 처리됩니다. 보고서에 식, 스크립트, 사용자 지정 보고서 항목 또는 사용자 지정 어셈블리가 포함된 경우 사용자의 자격 증명으로 코드가 실행됩니다. 스크립트가 포함된 HTML 문서가 리소스인 경우 사용자가 보고서 서버에서 문서를 열면 스크립트가 실행됩니다. 보고서에 있는 스크립트나 코드를 실행하는 기능은 강력한 기능으로서 위험 요소가 있을 수 있습니다. 악성 코드인 경우 보고서 서버와 보고서를 실행하는 사용자가 공격을 받을 수 있습니다.  
  
 HTML로 처리되는 보고서와 리소스에 대한 액세스 권한을 부여할 때는 보고서가 완전 신뢰 수준에서 처리되고 악의적인 스크립트가 클라이언트에 보내질 수 있다는 점을 기억해야 합니다. 브라우저 설정에 따라 클라이언트는 브라우저에 지정된 신뢰 수준에서 HTML을 실행합니다.  
  
 다음과 같은 예방 조치를 통해 악의적인 스크립트가 실행되는 위험을 줄일 수 있습니다.  
  
-   보고서 서버에 내용을 게시할 수 있는 사용자는 신중하게 결정합니다. 사용자가 악의적인 내용을 게시할 가능성이 있으므로 신뢰할 수 있는 소수의 사용자만 내용을 게시할 수 있도록 해야 합니다.  
  
-   모든 게시자는 출처를 알 수 없거나 신뢰할 수 없는 보고서와 리소스를 게시하지 말아야 합니다. 필요한 경우 텍스트 편집기에서 파일을 열고 의심스러운 스크립트와 URL을 찾습니다.  
  
## <a name="report-parameters-and-script-injection"></a>보고서 매개 변수 및 스크립트 삽입  
 보고서 매개 변수를 사용하면 보다 유연하게 보고서를 디자인하고 실행할 수 있습니다. 그러나 때로는 이러한 유연함이 공격자의 유인 공격에 이용될 수 있습니다. 악성 스크립트를 실수로 실행하는 위험을 줄이기 위해 신뢰할 수 있는 출처의 렌더링된 보고서만 여십시오. 잠재적 HTML 렌더러 스크립트 삽입 공격에 해당하는 다음 시나리오를 검토하는 것이 좋습니다.  
  
1.  악성 텍스트를 포함할 수 있는 매개 변수 값으로 하이퍼링크 동작이 설정된 입력란이 보고서에 포함되어 있습니다.  
  
2.  웹 페이지의 URL에서 보고서 매개 변수 값을 제어할 수 있는 방식으로 보고서가 보고서 서버에 게시되었거나 이와 같은 방식으로 보고서를 사용할 수 있습니다.  
  
3.  공격자가 웹 페이지 또는 형식에서 매개 변수의 값을 지정 하는 보고서 서버에 대 한 링크를 만듭니다 "javascript:\<악성 스크립트 >" 하 고 해당 링크를 유인 공격 다른 사람에 게 보냅니다.  
  
## <a name="mitigating-script-injection-attacks-in-a-hyperlink-in-a-published-report-or-document"></a>게시된 보고서 또는 문서의 하이퍼링크를 이용한 스크립트 삽입 공격 위험 완화  
 보고서의 보고서 항목 또는 보고서 항목의 일부에 대한 Action 속성 값에 하이퍼링크를 포함할 수 있습니다. 이러한 하이퍼링크는 보고서 처리 시 외부 데이터 원본에서 검색되는 데이터에 바인딩될 수 있습니다. 악의적 사용자가 이러한 기본 데이터를 수정할 경우 하이퍼링크는 스크립팅 악용 공격의 대상이 될 수 있습니다. 사용자가 게시된 보고서나 내보낸 보고서의 링크를 클릭하면 악성 스크립트가 실행될 수 있습니다.  
  
 보고서에 포함한 링크로 인해 실수로 악성 스크립트가 실행되는 위험을 완화하려면 신뢰할 수 있는 출처의 데이터에만 하이퍼링크를 바인딩하십시오. 쿼리 결과의 데이터 및 하이퍼링크에 데이터를 바인딩하는 식으로 악용될 수 있는 링크를 만들지 않았는지 확인하십시오. 예를 들어 여러 데이터 집합 필드의 데이터를 연결하는 식을 기반으로 하이퍼링크를 만들지 않도록 합니다. 필요한 경우 보고서에서 "원본 보기"를 사용하여 의심스러운 스크립트와 URL이 있는지 확인합니다.  
  
## <a name="mitigating-sql-injection-attacks-in-a-parameterized-report"></a>매개 변수가 있는 보고서의 SQL 삽입 공격 위험 완화  
 **String**형식의 매개 변수가 포함된 보고서에서는 유효한 값 목록이라고도 하는 사용 가능한 값 목록을 사용해야 하며 보고서를 실행하는 모든 사용자가 보고서의 데이터를 보는 데 필요한 권한만 갖도록 해야 합니다. **String**유형의 매개 변수를 정의할 경우 모든 값을 사용할 수 있는 입력란이 사용자에게 제공됩니다. 사용 가능한 값 목록은 입력할 수 있는 값을 제한합니다. 보고서 매개 변수가 쿼리 매개 변수에 연결되어 있고 사용 가능한 값 목록을 사용하지 않는 경우에는 보고서 사용자가 입력란에 SQL 구문을 입력할 수 있으므로 보고서와 서버가 SQL 인젝션 공격을 받을 가능성이 있습니다. 사용자에게 새 SQL 문 실행을 위한 충분한 권한이 있으면 서버에 원하지 않은 결과가 발생할 수 있습니다.  
  
 보고서 매개 변수가 쿼리 매개 변수에 연결되어 있지 않고 매개 변수 값이 보고서에 포함된 경우에는 보고서 사용자가 식 구문 또는 URL을 매개 변수 값에 입력하고 보고서를 Excel 또는 HTML로 렌더링할 수 있습니다. 이후 다른 사용자가 보고서를 보면서 렌더링된 매개 변수 내용을 클릭할 경우 악의적인 스크립트나 링크가 실수로 실행될 수 있습니다.  
  
 악의적인 스크립트를 실수로 실행하는 위험을 줄이기 위해 신뢰할 수 있는 원본의 렌더링된 보고서만 여세요.  
  
> [!NOTE]  
>  이전 버전의 설명서에는 동적 쿼리를 식으로 만드는 예가 포함되었습니다. 이러한 유형의 쿼리는 SQL 삽입 공격에 이용되기 쉬우므로 사용하지 않는 것이 좋습니다.  
  
## <a name="securing-confidential-reports"></a>기밀 보고서 보안  
 기밀 정보가 들어 있는 보고서의 경우 사용자에게 주요 데이터에 대한 액세스 자격 증명을 요청함으로써 데이터 액세스 수준에서 보안을 유지해야 합니다. 자세한 내용은 [Specify Credential and Connection Information for Report Data Sources](../../reporting-services/report-data/specify-credential-and-connection-information-for-report-data-sources.md)을 참조하세요. 권한이 없는 사용자가 액세스하지 못하도록 폴더에 보안을 지정할 수도 있습니다. 자세한 내용은 [폴더 보안](../../reporting-services/security/secure-folders.md)을 참조하세요.  
  
## <a name="see-also"></a>관련 항목:  
 [역할 할당 생성 및 관리](../../reporting-services/security/create-and-manage-role-assignments.md)   
 [보고서 작성기 액세스 구성](../../reporting-services/report-server/configure-report-builder-access.md)   
 [기본 모드 보고서 서버에 대한 사용 권한 부여](../../reporting-services/security/granting-permissions-on-a-native-mode-report-server.md)   
 [공유 데이터 원본 항목 보안 설정](../../reporting-services/security/secure-shared-data-source-items.md)   
 [Reporting Services 데이터 원본에 자격 증명 저장](../../reporting-services/report-data/store-credentials-in-a-reporting-services-data-source.md)  
  
  
