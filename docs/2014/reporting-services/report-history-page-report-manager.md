---
title: 보고서 기록 페이지 (보고서 관리자) | Microsoft Docs
ms.prod: sql-server-2014
ms.technology: reporting-services-native
ms.topic: conceptual
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.reviewer: ''
ms.custom: ''
ms.date: 06/13/2017
ms.openlocfilehash: 0b0841e031ee1a98f4f678406f790996a709e90f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66104477"
---
# <a name="report-history-page-report-manager"></a>보고서 기록 페이지(보고서 관리자)

보고서 기록 페이지를 사용하여 시간에 따라 생성 및 저장된 보고서 스냅샷을 볼 수 있습니다. 보고서 서버에 설정된 옵션에 따라 보고서 기록에 최근 스냅샷만 포함되어 있을 수 있습니다.  
  

보고서 기록은 항상 이 기록의 원본으로 사용되는 보고서의 컨텍스트 내에서 볼 수 있습니다. 보고서 서버의 모든 보고서 기록을 한 곳에서 볼 수는 없습니다.  
  
보고서 기록을 생성하려면 보고서가 무인 모드로 실행될 수 있어야 합니다. 즉, 보고서에서 저장된 자격 증명을 사용해야 하며, 매개 변수 있는 보고서의 경우 모든 매개 변수에 대한 기본 매개 변수 값을 포함해야 합니다. 보고서 기록은 수동으로 또는 예약된 작업으로 생성할 수 있습니다. 보고서의 기록 속성에 따라 보고서 기록을 만드는 방법이 지정됩니다.  
  
보고서 기록 스냅샷을 클릭하면 이 스냅샷을 볼 수 있습니다. 보고서 기록에 표시되는 스냅샷은 스냅샷이 만들어진 날짜와 시간으로만 구별됩니다. 스냅샷이 예약된 작업에 따라 생성된 것인지 수동 작업으로 생성된 것인지는 시각적으로 구분할 수 없습니다.  
  
> [!NOTE]  
>  이 기능은 일부 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]버전에서는 사용할 수 없습니다. 버전에서 지원 되는 기능 목록은 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [SQL Server 2014 버전에서 지 원하는 기능](../../2014/getting-started/features-supported-by-the-editions-of-sql-server-2014.md)을 참조 하세요.  
  
## <a name="navigation"></a>탐색  
 사용자 인터페이스(UI)에서 이 위치를 탐색하려면 다음 절차를 사용하십시오.  
  
### <a name="to-open-the-report-history-page"></a>보고서 기록 페이지를 열려면  
  
1.  보고서 관리자를 열고 보고서 스냅샷을 보려는 보고서를 찾습니다.  
  
2.  보고서 위로 마우스를 이동하여 드롭다운 화살표를 클릭합니다.  
  
3.  드롭다운 메뉴에서 **보고서 기록 보기**를 클릭합니다.  
  
## <a name="options"></a>옵션  
 **Delete**  
 하나 이상의 스냅샷을 삭제하려면 클릭합니다. 
  **삭제**를 클릭하기 전에 삭제할 스냅샷 옆의 확인란을 선택하십시오.  
  
 **새 스냅숏**  
 보고서 기록에 스냅샷을 추가하려면 클릭합니다. 이 단추는 보고서의 기록 속성 페이지에서 **수동으로 기록 작성 허용** 옵션을 선택하는 경우에 사용할 수 있습니다.  
  
 **마지막 실행**  
 스냅샷이 만들어진 날짜와 시간을 표시합니다. 특정 스냅샷을 보려면 설명을 클릭하십시오.  
  
 **크기**  
 보고서 정의와 보고서 데이터를 합한 크기를 표시합니다. 이 값은 보고서 정의와 데이터에서 사용하는 보고서 서버 데이터베이스 공간 크기를 나타냅니다. 서식을 포함하는 렌더링된 보고서의 크기는 실제로 더 큽니다. 괄호 안에 표시된 전체 크기는 현재 보고서에 대한 보고서 기록의 모든 스냅샷 크기의 합계입니다.  
  
## <a name="see-also"></a>참고 항목  
 [보고서 기록을 보거나 삭제 &#40;보고서 관리자&#41;](../../2014/reporting-services/view-or-delete-report-history-report-manager.md)   
 [보고서 기록에 스냅샷 추가&#40;보고서 관리자&#41;](report-server/add-a-snapshot-to-report-history-report-manager.md)   
 [일반 속성 페이지, 보고서 &#40;보고서 관리자&#41;](../../2014/reporting-services/general-properties-page-reports-report-manager.md)   
 [F1 도움말 보고서 관리자](../../2014/reporting-services/report-manager-f1-help.md)   
 [스냅숏 옵션 속성 페이지 &#40;보고서 관리자&#41;](../../2014/reporting-services/snapshot-options-properties-page-report-manager.md)