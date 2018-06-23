---
title: 새 데이터 원본 페이지 (보고서 관리자) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 35563d4c-a3d5-4f95-bf46-605da9dfcbb8
caps.latest.revision: 33
author: markingmyname
ms.author: maghan
manager: mblythe
ms.openlocfilehash: 4c951f5dbf663d7a6f55b493aeac86cd32c0f72a
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36091675"
---
# <a name="new-data-source-page-report-manager"></a>새 데이터 원본 페이지(보고서 관리자)
  새 데이터 원본 페이지를 사용하여 공유 데이터 원본 항목을 만들 수 있습니다. 공유 데이터 원본은 외부 데이터 원본과의 연결을 정의합니다. 공유 데이터 원본을 사용하면 해당 데이터 원본을 사용하는 보고서, 모델 및 데이터 기반 구독과는 별도로 데이터 원본 연결에 대한 설정을 만들고 관리할 수 있습니다.  
  
## <a name="navigation"></a>탐색  
 사용자 인터페이스(UI)에서 이 위치를 탐색하려면 다음 절차를 사용하십시오.  
  
###### <a name="to-open-the-new-data-source-page"></a>새 데이터 원본 페이지를 열려면  
  
1.  보고서 관리자를 열고 데이터 원본을 만들려는 폴더로 이동합니다.  
  
2.  도구 모음에서 **새 데이터 원본**을 클릭합니다. 공유 데이터 원본을 만들려면 내용 관리자 권한이 있어야 합니다.  
  
## <a name="options"></a>변수  
 **이름**  
 보고서 서버 폴더 계층 구조에서 항목을 식별하는 데 사용되는 공유 데이터 원본의 이름을 입력합니다.  
  
 **설명**  
 공유 데이터 원본에 대한 정보를 제공합니다. 이 설명은 내용 페이지에 표시됩니다.  
  
 **목록 뷰에서 숨기기**  
 보고서 관리자에서 목록 뷰 모드를 사용하는 사용자가 볼 수 없게 공유 데이터 원본을 숨기려면 이 옵션을 선택합니다. 목록 뷰 모드는 보고서 서버 폴더 계층을 검색할 때 표시되는 기본 뷰 형식입니다. 목록 뷰에서 항목 이름과 설명은 페이지에 가로로 표시됩니다. 이 외에도 자세히 보기를 사용할 수 있습니다. 자세히 보기는 설명을 표시하지 않지만 항목에 대한 다른 정보는 포함합니다. 목록 뷰에서는 항목을 숨길 수 있지만 자세히 보기에서는 항목을 숨길 수 없습니다. 항목에 대한 액세스를 제한하려면 역할 할당을 만들어야 합니다.  
  
 **이 데이터 원본 사용**  
 공유 데이터 원본을 설정 또는 해제하도록 선택합니다. 공유 데이터 원본을 해제하여 항목을 참조하는 모든 보고서 및 모델이 처리되지 않도록 할 수 있습니다.  
  
 **데이터 원본 유형**  
 데이터 원본의 데이터를 처리하는 데 사용되는 데이터 처리 확장 프로그램을 지정합니다. 보고서 서버에 대 한 데이터 처리 확장 프로그램이 포함 되어 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], Oracle, [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)], SAP, XML, ODBC 및 OLE DB 합니다. 다른 데이터 처리 확장 프로그램은 관련 공급업체로부터 구할 수 있습니다.  
  
 원격 및 비 SQL 데이터 원본 지원에 대 한 자세한 내용은 참조 [SQL Server 2012 버전에서 지 원하는 기능](http://go.microsoft.com/fwlink/?linkid=232473) (HYPERLINK "http://go.microsoft.com/fwlink/?linkid=232473" http://go.microsoft.com/fwlink/?linkid=232473) 및 [보고에서 데이터 원본 지원 서비스 &#40;SSRS&#41;](create-deploy-and-manage-mobile-and-paginated-reports.md)합니다.  
  
 **연결 문자열**  
 보고서 서버가 데이터 원본에 연결하는 데 사용하는 연결 문자열을 지정합니다. 연결 형식에 따라 사용하는 구문이 결정됩니다. 예를 들어 XML 데이터 처리 확장 프로그램에 대한 연결 문자열은 XML 문서에 대한 URL입니다. 대부분의 경우 일반적인 연결 문자열은 데이터베이스 서버와 데이터 파일을 지정합니다.  
  
 다음 예제에서는 연결 문자열에 연결 하는 데 사용 된 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssSampleDBnormal](../includes/sssampledbnormal-md.md)] 데이터베이스:  
  
```  
data source=<a SQL Server instance>;initial catalog=AdventureWorks2012  
```  
  
 자세한 예제 및 연결 문자열을 지정 하 여 다양 한 방법에 대 한 정보를 참조 하세요. [데이터 연결, 데이터 원본 및 Reporting Services의 연결 문자열](../../2014/reporting-services/data-connections-data-sources-and-connection-strings-in-reporting-services.md)합니다.  
  
 **사용 하 여 연결**  
 자격 증명을 가져오는 방법을 결정하는 옵션을 지정합니다.  
  
> [!IMPORTANT]  
>  연결 문자열에 자격 증명이 제공된 경우 이 섹션에서 제공한 옵션 및 값은 무시됩니다. 연결 문자열에서 자격 증명을 지정하는 경우 값은 이 페이지를 보는 모든 사용자에게 일반 텍스트로 표시됩니다.  
  
 **(연결 방법) 보고서를 실행 하는 사용자가 제공한 자격 증명**  
 데이터 원본에 액세스하려면 사용자 이름과 암호를 입력하라는 메시지가 각 사용자에게 표시됩니다. 사용자 자격 증명을 요청하는 프롬프트 텍스트를 정의할 수 있습니다. 기본 텍스트 문자열은 "데이터 원본에 액세스하려면 사용자 이름 및 암호를 입력하십시오."입니다.  
  
 사용자가 제공하는 자격 증명이 Windows 인증 자격 증명인 경우 **데이터 원본에 연결할 때 Windows 자격 증명으로 사용** 을 선택합니다. 데이터베이스 인증을 사용 하는 경우이 확인란을 선택 하지 마십시오 (예를 들어 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 인증).  
  
 **(연결 방법) 보고서 서버에 안전 하 게 저장 된 자격 증명**  
 암호화된 사용자 이름 및 암호를 보고서 서버 데이터베이스에 저장합니다. 사용자 동작이 아닌 일정 또는 이벤트로 시작되는 보고서와 같이 무인 모드로 보고서를 실행하려는 경우 이 옵션을 선택합니다. 기본 보안을 사용하는 경우 사용자 이름은 Windows 도메인 계정이어야 합니다. 이 형식으로 계정을 지정: \<도메인 >\\< 사용자 이름\>합니다. 지정하는 계정에는 보고서에 사용되는 데이터 원본을 호스팅하는 컴퓨터에 대한 로컬 로그온 권한이 있어야 합니다.  
  
 자격 증명이 Windows 인증 자격 증명인 경우 **데이터 원본에 연결할 때 Windows 자격 증명으로 사용** 을 선택합니다. 데이터베이스 인증을 사용 하는 경우이 확인란을 선택 하지 마십시오 (예를 들어 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 인증).  
  
 데이터베이스 인증을 사용하는 경우 데이터베이스 자격 증명 위임을 허용하려면 데이터베이스 서버에서 가장을 지원하는 경우에만 **데이터 원본에 연결한 후 인증된 사용자로 가장** 을 선택하십시오. 에 대 한 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 데이터베이스의 경우이 옵션은 SETUSER 함수를 설정 합니다.  
  
 **Windows 통합된 보안 (연결 방법)**  
 현재 사용자의 Windows 자격 증명을 사용하여 데이터 원본에 액세스합니다. 데이터 원본에 액세스하는 데 사용되는 자격 증명이 네트워크 도메인에 로그온하는 데 사용되는 자격 증명과 같으면 이 옵션을 선택합니다. 이 옵션은 도메인에 Kerberos 인증을 설정한 경우나 데이터 원본이 보고서 서버와 같은 컴퓨터에 있는 경우에 가장 잘 작동합니다. Kerberos 인증을 해제하면 Windows 자격 증명이 다른 컴퓨터로 전달될 수 있습니다. 컴퓨터 연결이 추가로 필요한 경우에는 원하는 데이터가 아닌 오류가 반환됩니다.  
  
 보고서 서버 관리자는 보고서 데이터 원본 액세스에 Windows 통합 보안을 사용하지 못하도록 설정할 수 있습니다. 이 값이 회색으로 나타나면 해당 기능을 사용할 수 없는 것입니다.  
  
 이 보고서를 예약 또는 구독하려는 경우 이 옵션을 사용하지 마십시오. 예약된 보고서 처리 또는 무인 보고서 처리를 위해서는 사용자 입력이나 현재 사용자의 보안 컨텍스트 없이 얻을 수 있는 자격 증명이 필요합니다. 저장된 자격 증명만 이 기능을 제공합니다. 따라서 보고서가 Windows 통합 보안 자격 증명 유형으로 구성된 경우 보고서 서버는 보고서 처리나 구독 처리를 예약할 수 없도록 차단합니다. 이미 구독되는 보고서 또는 예약된 작업이 있는 보고서에 대해 이 옵션을 선택하면 해당 구독 및 예약된 작업이 중지됩니다.  
  
 **자격 증명 필요 없음 (연결 방법)**  
 자격 증명 없이 데이터 원본에 액세스할 수 있도록 지정합니다. 데이터 원본에 사용자 로그온이 필요한 경우에는 이 옵션을 선택해도 적용되지 않습니다. 데이터 원본 연결에 사용자 자격 증명이 필요하지 않은 경우에만 이 옵션을 선택해야 합니다.  
  
 이 옵션을 사용하려면 보고서 서버 배포를 위한 무인 실행 계정을 먼저 구성해야 합니다. 무인 실행 계정은 다른 자격 증명 원본을 사용할 수 없는 경우 외부 데이터 원본에 연결하는 데 사용됩니다. 이 옵션을 지정하고 계정을 구성하지 않으면 보고서 데이터 원본에 연결하지 못하고 보고서가 처리되지 않습니다. 이 계정에 대 한 자세한 내용은 참조 [무인 실행 계정을 구성 &#40;SSRS 구성 관리자&#41;](install-windows/configure-the-unattended-execution-account-ssrs-configuration-manager.md)합니다.  
  
 **확인**  
 클릭하여 변경 내용을 저장합니다.  
  
## <a name="see-also"></a>관련 항목  
 [만들기, 삭제 또는 공유 데이터 원본을 수정 &#40;보고서 관리자&#41;](../../2014/reporting-services/create-delete-or-modify-a-shared-data-source-report-manager.md)   
 [데이터 연결, 데이터 원본 및 Reporting Services의 연결 문자열](../../2014/reporting-services/data-connections-data-sources-and-connection-strings-in-reporting-services.md)   
 [보고서 관리자 &#40;SSRS 기본 모드&#41;](../../2014/reporting-services/report-manager-ssrs-native-mode.md)   
 [페이지 콘텐츠 &#40;보고서 관리자&#41;](../../2014/reporting-services/contents-page-report-manager.md)   
 [만들기, 수정 및 공유 데이터 원본을 삭제 &#40;SSRS&#41;](report-data/create-modify-and-delete-shared-data-sources-ssrs.md)   
 [보고서 관리자 F1 도움말](../../2014/reporting-services/report-manager-f1-help.md)   
 [보고서 데이터 원본에 대한 자격 증명 및 연결 정보 지정](report-data/specify-credential-and-connection-information-for-report-data-sources.md)  
  
  