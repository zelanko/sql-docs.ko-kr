---
title: 기본 제공 Globals 및 Users 참조(보고서 작성기 및 SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 5f5e1149-c967-454d-9a63-18ec4a33d985
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: ef0438dfa0750c2a516a801a2d81b5d1c0b49721
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66106436"
---
# <a name="built-in-globals-and-users-references-report-builder-and-ssrs"></a>기본 제공 Globals 및 Users 참조(보고서 작성기 및 SSRS)
  `Globals` 및 `User` 컬렉션을 모두 포함하는 기본 제공 필드 컬렉션은 보고서를 처리할 때 Reporting Services에서 제공하는 전역 값을 나타냅니다. `Globals` 컬렉션은 보고서의 이름, 보고서 처리가 시작된 시간, 보고서 머리글 또는 바닥글의 현재 페이지 번호와 같은 값을 제공합니다. `User` 컬렉션은 사용자 식별자 및 언어 설정을 제공합니다. 이러한 값을 식에 사용하여 보고서의 결과를 필터링할 수 있습니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="using-the-globals-collection"></a>전역 컬렉션 사용  
 `Globals` 컬렉션에는 보고서의 전역 변수가 포함됩니다. 디자인 화면에서 이러한 변수는 &(앰퍼샌드) 접두사가 붙은 상태로 표시됩니다(예: `[&ReportName]`). 다음 표에서는 `Globals` 컬렉션의 멤버를 설명합니다.  
  
|**멤버**|**형식**|**설명**|  
|----------------|--------------|---------------------|  
|ExecutionTime|`DateTime`|보고서가 실행되기 시작한 날짜와 시간입니다.|  
|PageNumber|`Integer`|페이지 번호를 다시 설정하는 페이지 나누기를 기준으로 한 현재 페이지 번호입니다. 보고서 처리를 시작할 때 초기 값은 -1로 설정됩니다. 페이지 번호는 각 렌더링된 페이지에 대해 증가합니다.<br /><br /> 사각형, 데이터 영역, 데이터 영역 그룹 또는 지도 PageBreak 속성에 대 한 페이지 나누기 내에서 페이지 번호 ResetPageNumber 속성을 설정 `True`합니다. 테이블릭스 열 계층 구조 그룹에는 지원되지 않습니다.<br /><br /> PageNumber는 페이지 머리글 또는 페이지 바닥글의 식에만 사용할 수 있습니다.|  
|ReportFolder|`String`|보고서를 포함하는 폴더의 전체 경로입니다. 여기에는 보고서 서버 URL이 포함되지 않습니다.|  
|ReportName|`String`|보고서 서버 데이터베이스에 저장되어 있는 보고서의 이름입니다.|  
|ReportServerUrl|`String`|보고서가 실행 중인 보고서 서버의 URL입니다.|  
|TotalPages|`Integer`|PageNumber를 다시 설정하는 페이지 나누기를 기준으로 한 총 페이지 수입니다. 페이지 나누기가 설정되어 있지 않으면 이 값은 OverallTotalPages와 같습니다.<br /><br /> TotalPages는 페이지 머리글 또는 페이지 바닥글의 식에만 사용할 수 있습니다.|  
|PageName|`String`|페이지의 이름입니다. 보고서 처리를 시작할 때 초기 값은 InitialPageName(보고서 속성)에서 설정됩니다. 각 보고서 항목을 처리하면 이 값은 사각형, 데이터 영역, 데이터 영역 그룹 또는 지도의 해당 PageName 값으로 바뀝니다. 테이블릭스 열 계층 구조 그룹에는 지원되지 않습니다.<br /><br /> PageName은 페이지 머리글 또는 페이지 바닥글의 식에만 사용할 수 있습니다.|  
|OverallPageNumber|`Integer`|전체 보고서에서 현재 페이지의 페이지 번호입니다. 이 값은 ResetPageNumber의 영향을 받지 않습니다.<br /><br /> OverallPageNumber는 페이지 머리글 또는 페이지 바닥글의 식에만 사용할 수 있습니다.|  
|OverallTotalPages|`Integer`|전체 보고서의 총 페이지 수입니다. 이 값은 ResetPageNumber의 영향을 받지 않습니다.<br /><br /> OverallTotalPages는 페이지 머리글 또는 페이지 바닥글의 식에만 사용할 수 있습니다.|  
|RenderFormat|`RenderFormat`|현재 렌더링 요청에 대한 정보입니다.<br /><br /> 자세한 내용은 다음 섹션의 "RenderFormat"을 참조하십시오.|  
  
 `Globals` 컬렉션 멤버는 variant를 반환합니다. 특정 데이터 형식이 필요한 식에서 이 컬렉션의 멤버를 사용하려면 먼저 변수를 캐스팅해야 합니다. 예를 들어 실행 시간 variant를 날짜 형식으로 변환하려면 `=CDate(Globals!ExecutionTime)`를 사용합니다. 자세한 내용은 [식의 데이터 형식&#40;보고서 작성기 및 SSRS&#41;](expressions-report-builder-and-ssrs.md)).  
  
### <a name="renderformat"></a>RenderFormat  
 다음 표에서는 `RenderFormat`의 멤버에 대해 설명합니다.  
  
|멤버|형식|Description|  
|------------|----------|-----------------|  
|이름|`String`|RSReportServer 구성 파일에 등록된 렌더러 이름입니다.<br /><br /> 보고서 처리/렌더링 주기의 특정 부분에서 사용 가능합니다.|  
|IsInteractive|`Boolean`|현재 렌더링 요청이 대화형 렌더링 형식을 사용하는지 여부입니다.|  
|DeviceInfo|읽기 전용 이름/값 컬렉션|현재 렌더링 요청에 대한 deviceinfo 매개 변수의 키/값 쌍입니다.<br /><br /> 컬렉션에 키나 인덱스를 사용해 문자열 값을 지정할 수 있습니다.|  
  
### <a name="examples"></a>예  
 다음 예에서는 식에서 `Globals` 컬렉션에 대한 참조를 사용하는 방법을 보여 줍니다.  
  
-   이 식을 보고서 바닥글의 입력란에 배치하면 보고서의 페이지 번호와 총 페이지 수가 제공됩니다.  
  
     `=Globals.PageNumber & " of " & Globals.TotalPages`  
  
-   이 식은 보고서 이름과 보고서가 실행된 시간을 제공합니다. 시간 형식은 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 형식 문자열(간단한 날짜)로 지정됩니다.  
  
     `=Globals.ReportName & ", dated " & Format(Globals.ExecutionTime, "d")`  
  
-   보고서를 Excel로 내보낼 때 선택한 열에 대해 **열 표시 유형** 대화 상자에 배치된 식은 열을 표시합니다. 그렇지 않은 경우 이 열은 숨겨집니다.  
  
     `EXCELOPENXML` 은 Office 2007에 포함된 Excel 형식을 나타냅니다. `EXCEL` 은 Office 2003에 포함된 Excel 형식을 나타냅니다.  
  
     `=IIF(Globals!RenderFormat.Name = "EXCELOPENXML" OR Globals!RenderFormat.Name = "EXCEL", false, true)`  
  
## <a name="using-the-user-collection"></a>User 컬렉션 사용  
 `User` 컬렉션에는 보고서를 실행하는 사용자에 대한 데이터가 포함됩니다. 예를 들어 이 컬렉션을 사용하여 보고서에 나타나는 데이터를 필터링함으로써 현재 사용자의 데이터만 표시하거나 보고서 제목 등에 UserID를 표시할 수 있습니다. 디자인 화면에서 이러한 변수는 &(앰퍼샌드) 접두사가 붙은 상태로 표시됩니다(예: `[&UserID]`).  
  
 다음 표에서는 `User` 컬렉션의 멤버를 설명합니다.  
  
|**멤버**|**형식**|**설명**|  
|----------------|--------------|---------------------|  
|`Language`|`String`|보고서를 실행하는 사용자의 `en-US`) 을 입력합니다.|  
|`UserID`|`String`|보고서를 실행하는 사용자의 ID입니다. Windows 인증을 사용하는 경우 이 값은 현재 사용자의 도메인 계정입니다. 값은 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 보안 확장 프로그램에 의해 결정되며 이 프로그램은 Windows 인증 또는 사용자 지정 인증을 사용할 수 있습니다.|  
  
 보고서에서 여러 언어를 지원하는 방법에 대한 자세한 내용은 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SQL Server 온라인 설명서 [의](https://go.microsoft.com/fwlink/?LinkId=120955)설명서에서 "다국어 배포 또는 글로벌 배포를 위한 솔루션 디자인 고려 사항"을 참조하세요.  
  
### <a name="using-locale-settings"></a>로캘 설정 사용  
 식을 사용하여 `User.Language` 값을 통해 클라이언트 컴퓨터의 로캘 설정을 참조하여 보고서가 사용자에게 표시되는 방식을 결정할 수 있습니다. 예를 들어 로캘 값에 따라 다른 쿼리 식을 사용하는 보고서를 만들 수 있습니다. 반환되는 언어에 따라 다양한 열에서 지역화된 정보를 검색하기 위해 쿼리가 변경될 수 있습니다. 또한 이 변수를 기반으로 하는 보고서나 보고서 항목의 언어 설정에 식을 사용할 수 있습니다.  
  
> [!NOTE]  
>  보고서의 언어 설정을 변경할 수 있지만 이로 인한 표시 문제에 유의해야 합니다. 예를 들어 보고서의 로캘 설정을 변경하면 보고서의 날짜 형식을 변경할 수 있지만 통화 형식도 변경될 수 있습니다. 통화가 적절하게 변환되지 않으면 잘못된 통화 기호가 보고서에 표시될 수 있습니다. 이를 방지하려면 변경할 개별 항목에 대한 언어 정보를 설정하거나 통화 데이터가 있는 항목을 특정 언어로 설정합니다.  
  
### <a name="identifying-userid-for-snapshot-or-history-reports"></a>스냅숏 또는 기록 보고서에 대한 UserID 식별  
 *User!UserID* 변수를 포함하는 보고서에서는 보고서를 보고 있는 현재 사용자와 관련된 보고서 데이터가 표시되지 않는 경우도 있습니다.  
  
## <a name="see-also"></a>관련 항목  
 [식&#40;보고서 작성기 및 SSRS&#41;](expressions-report-builder-and-ssrs.md)   
 [식 대화 상자&#40;보고서 작성기&#41;](../expression-dialog-box-report-builder.md)   
 [식의 데이터 형식&#40;보고서 작성기 및 SSRS&#41;](expressions-report-builder-and-ssrs.md)   
 [숫자 및 날짜 서식 지정&#40;보고서 작성기 및 SSRS&#41;](formatting-numbers-and-dates-report-builder-and-ssrs.md)   
 [식 예&#40;보고서 작성기 및 SSRS&#41;](expression-examples-report-builder-and-ssrs.md)  
  
  
