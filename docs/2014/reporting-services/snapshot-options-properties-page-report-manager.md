---
title: 스냅숏 옵션 속성 페이지 (보고서 관리자) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: f6641f59-5267-4f57-8957-63b93d1a9679
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 4a18e523c8d839cc6ec9e0c64c94ad648b1c1d0c
ms.sourcegitcommit: 8d6fb6bbe3491925909b83103c409effa006df88
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/22/2019
ms.locfileid: "59954349"
---
# <a name="snapshot-options-properties-page-report-manager"></a>스냅숏 옵션 속성 페이지(보고서 관리자)
  스냅숏 옵션 속성 페이지를 사용하여 보고서 스냅숏이 보고서 기록에 추가되는 일정을 예약할 수 있고 보고서 기록에 저장되는 보고서 스냅숏 수에 제한을 설정할 수 있습니다.  
  
> [!NOTE]  
>  이 기능은 일부 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]버전에서는 사용할 수 없습니다. 버전에서 지원 되는 기능 목록은 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]를 참조 하세요 [추가 데이터베이스 서비스](../../2014/getting-started/features-supported-by-the-editions-of-sql-server-2014.md#Add_DBServices)합니다.  
  
## <a name="navigation"></a>탐색  
 사용자 인터페이스(UI)에서 이 위치를 탐색하려면 다음 절차를 사용하십시오.  
  
### <a name="to-open-the-snapshot-options-properties-page-for-a-report"></a>보고서의 스냅숏 옵션 속성 페이지를 열려면  
  
1.  보고서 관리자를 열고 보고서 스냅숏 속성을 구성할 보고서를 찾습니다.  
  
2.  보고서 위로 마우스를 이동하여 드롭다운 화살표를 클릭합니다.  
  
3.  드롭다운 메뉴에서 **관리**를 클릭합니다. 보고서의 일반 속성 페이지가 열립니다.  
  
4.  **스냅숏 옵션** 탭을 선택합니다.  
  
## <a name="options"></a>변수  
 **수동으로 보고서 기록 허용**  
 필요에 따라 스냅숏을 보고서 기록에 추가하려면 이 확인란을 선택합니다. 이 확인란을 선택하면 기록 페이지에 **새 스냅숏** 단추가 표시됩니다.  
  
 **모든 보고서 실행 스냅숏을 보고서 기록에 저장**  
 보고서 실행 속성에 따라 생성하는 보고서 스냅숏을 보고서 기록에 복사하려면 이 확인란을 선택합니다. 생성된 스냅숏에서 보고서를 실행하도록 보고서 실행 속성을 설정할 수 있습니다. 이 보고서 기록 속성을 설정하면 스냅숏의 복사본을 보고서 기록에 저장하여 시간에 따라 생성되는 모든 보고서 스냅숏에 대한 기록을 보관할 수 있습니다.  
  
 **다음 일정을 사용 하 여 스냅숏을 보고서 기록에 추가 하려면**  
 일정에 따라 스냅숏을 보고서 기록에 추가하려면 이 확인란을 선택합니다. 이 용도로 사용되는 일정을 따로 만들 수도 있고 원하는 일정 정보가 포함된 경우 미리 정의된 공유 일정에서 선택할 수도 있습니다.  
  
 **보관할 스냅숏 개수 선택**  
 보고서 기록에 보관되는 보고서 개수를 제어하려면 다음 옵션 중에서 선택합니다. 보고서 기록 설정은 보고서마다 다를 수 있습니다.  
  
-   기본 설정을 유지하려면 **기본 설정 사용** 을 선택하십시오. 보고서 서버 관리자가 보고서 기록 스토리지에 대한 마스터 설정을 제어합니다. 이 옵션을 선택하는 경우 보존되는 스냅숏의 개수는 이 마스터 설정에서 가져옵니다.  
  
-   모든 보고서 기록 스냅숏을 보존하려면 **보고서 기록에 스냅숏을 무제한 보관** 을 선택하십시오. 보고서 기록 크기를 줄이려면 스냅숏을 수동으로 삭제해야 합니다.  
  
-   설정된 개수의 스냅숏을 보존하려면 **보고서 기록의 복사본 개수 제한** 을 선택하십시오. 한도에 이르면 새 복사본의 저장 공간을 만들기 위해 보고서 기록에서 오래된 복사본이 제거됩니다.  
  
 보고서 기록은 보고서 서버 데이터베이스에 저장됩니다. 기록을 유지하려는 보고서의 수가 많거나 용량이 큰 경우 보고서 서버 데이터베이스의 디스크 공간 요구 사항을 관리하기 쉽도록 보고서 기록의 크기를 제한하는 것이 좋습니다.  
  
 **적용**  
 클릭하여 변경 내용을 저장합니다.  
  
## <a name="see-also"></a>관련 항목  
 [보고서 기록에 스냅숏 추가&#40;보고서 관리자&#41;](report-server/add-a-snapshot-to-report-history-report-manager.md)   
 [보고서 관리자&#40;SSRS 기본 모드&#41;](../../2014/reporting-services/report-manager-ssrs-native-mode.md)   
 [보고서 기록에서 스냅숏 만들기, 수정 및 삭제](report-server/create-modify-and-delete-snapshots-in-report-history.md)   
 [보고서 관리자 F1 도움말](../../2014/reporting-services/report-manager-f1-help.md)  
  
  
