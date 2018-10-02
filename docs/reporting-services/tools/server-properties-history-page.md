---
title: 서버 속성(기록 페이지) | Microsoft Docs
ms.date: 06/10/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: tools
ms.topic: conceptual
f1_keywords:
- sql13.swb.reportserver.serverproperties.history.f1
ms.assetid: be9d8018-a46f-4625-9ae1-138ebe6b38ba
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 498bc994828c4ed7089a4aa223659f70d1c612b5
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47663901"
---
# <a name="server-properties-history-page"></a>서버 속성(기록 페이지)
  [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] 에서 이 [!INCLUDE[ssManStudioFull_md](../../includes/ssmanstudiofull-md.md)] 페이지를 사용하여 보관할 보고서 기록 복사본 수의 기본값을 설정할 수 있습니다. 이 기본값은 모든 보고서에 대한 보고서 기록 제한을 설정하는 초기 설정이 됩니다. 이 설정은 보고서마다 다르게 설정할 수 있습니다.  
  
 보고서 기록은 스냅숏이 만들어진 시점의 보고서에 대한 현재 보고서 데이터 및 레이아웃을 포함하는 보고서 스냅숏 모음입니다. 보고서 기록을 사용하여 특정 날짜 또는 시간의 보고서 복사본을 유지할 수 있습니다. 기본 모드 보고서 서버, 또는 SharePoint 통합 모드로 구성된 보고서 서버에서 실행되는 개별 보고서에 대해 보고서 기록을 만들고 관리할 수 있습니다.  
  
 보고서 기록 스냅숏은 보고서 서버 데이터베이스에 저장됩니다. 스냅숏을 무제한으로 보관하는 경우 데이터베이스 크기를 정기적으로 점검하여 너무 빠른 속도로 커지거나 지나치게 많은 디스크 공간을 소모하지 않도록 하십시오.  
  
 이 페이지를 열려면
 1) [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]를 시작합니다.
 2) 보고서 서버 인스턴스에 연결합니다.
 3) 보고서 서버 이름을 마우스 오른쪽 단추로 클릭한 다음 **속성**을 선택합니다.
 4) **기록** 을 클릭하여 이 페이지를 엽니다.  
  
## <a name="options"></a>Options  
 **보고서 기록에 스냅숏을 무제한으로 보관**  
 모든 보고서 기록 스냅숏을 유지합니다. 보고서 기록 크기를 줄이려면 스냅숏을 수동으로 삭제해야 합니다.  
  
 **보고서 기록의 복사본 개수 제한**  
 설정된 수의 보고서 기록 스냅숏을 유지합니다. 한도에 이르면 새 복사본의 저장 공간을 만들기 위해 보고서 기록에서 오래된 복사본이 제거됩니다.  
  
 나중에 보고서 기록을 제한하면 기존 보고서 기록이 지정한 제한을 초과하는 경우 보고서 서버에서 기존 보고서 기록을 새 제한으로 축소합니다. 가장 오래된 보고서 스냅숏이 먼저 삭제됩니다. 보고서 기록이 비어 있거나 제한보다 적은 경우 새 보고서 스냅숏이 추가됩니다. 한도에 이르면 새 보고서 스냅숏이 추가될 때 가장 오래된 스냅숏이 삭제됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [보고서 서버 속성 설정&#40;Management Studio&#41;](../../reporting-services/tools/set-report-server-properties-management-studio.md)   
 [Management Studio에서 보고서 서버에 연결](../../reporting-services/tools/connect-to-a-report-server-in-management-studio.md)   
 [Management Studio의 보고서 서버 F1 도움말](../../reporting-services/tools/report-server-in-management-studio-f1-help.md)  
  
  
