---
title: 원본 제어 옵션 설정 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- VS.ToolsOptionsPages.Source_Control.Visual_SourceSafe
- VS.ToolsOptionsPages.Source_Control.General
- VS.ToolsOptionsPages.Source_Control.Environment
helpviewer_keywords:
- source controls [SQL Server Management Studio], options
ms.assetid: b2c6ca00-46f0-4f86-b067-07bae779c147
caps.latest.revision: 23
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 936b3b47050985d6d8507205a88c85a49cbbdd90
ms.sourcegitcommit: 8ae6e6618a7e9186aab3c6a37ea43776aa9a382b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/06/2018
ms.locfileid: "43817239"
---
# <a name="set-source-control-options"></a>원본 제어 옵션 설정
  [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]에 내장된 원본 제어 기능을 활용하기 전에 작업을 수행하는 다양한 환경에 대한 원본 제어 옵션을 구성해야 합니다.  
  
 사용 하 여 원본 제어 옵션을 구성 합니다 **옵션** 대화 상자를 하나 이상의 원본 제어 역할을 구성할 수 있습니다. 역할은 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]에 적용되는 설정에 대한 일반적인 설명과 해당 설정에 연결된 원본 제어 옵션으로 구성됩니다.  
  
 예를 들어 독자적 데이터베이스 개발자인 경우 일반적으로 파일을 체크 인한 후에 파일을 체크 아웃된 상태로 유지함으로써 다른 사용자와의 충돌을 방지합니다. 결과적으로 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]는 독자적 개발자 역할을 정의합니다. 이 역할에 대 한 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 자동으로 선택 합니다 **항목을 체크 인할 때 체크 아웃 상태로 유지** 옵션입니다.  
  
 역할을 정의하고 사용자 지정할 수 있기 때문에 특정 설정에서 다른 설정으로 이동할 때마다 원본 제어를 완전히 다시 구성할 필요 없이 다양한 개발 설정에서 작업할 수 있습니다.  
  
### <a name="to-set-source-control-options"></a>원본 제어 옵션을 설정하려면  
  
1.  **도구** 메뉴에서 **옵션**을 클릭합니다.  
  
2.  에 **옵션** 대화 상자에서 **소스 제어**를 클릭 하 고는 **플러그 인 선택** 페이지입니다.  
  
     **현재 소스 제어 플러그 인**  
     사용할 원본 제어를 이 목록에서 선택합니다. 컴퓨터에 설치되어 있는 원본 제어 제품 클라이언트만 목록에 나타납니다. 컴퓨터에 원본 제어 클라이언트가 설치되어 있지 않으면 없음만 표시됩니다. Microsoft Source Safe를 설치한 경우 다음 플러그 인이 표시됩니다.  
  
    -   Microsoft Visual SourceSafe  
  
    -   Microsoft Visual SourceSafe(Internet)  
  
3.  사용하려는 각 원본 제어 역할에 대한 로그인 자격 증명을 설정합니다. 이 페이지는 원본 제어 플러그 인이 설치된 경우에만 사용할 수 있습니다.  
  
     **역할 설명**  
     이 역할 중 하나를 선택하면 적절한 원본 제어 옵션이 자동으로 선택됩니다.  
  
    |역할|Description|  
    |----------|-----------------|  
    |**Visual SourceSafe**|가장 일반적으로 사용 되는 설정을 사용 하려는 지정 [!INCLUDE[msCoName](../includes/msconame-md.md)] Visual SourceSafe 사용자입니다.|  
    |**독자적 개발자**|사용자가 독자적으로 작업하도록 지정합니다.|  
    |**Custom**|사용자가 역할에 대한 설정을 수정했음을 나타냅니다.|  
  
     **백그라운드 상태 업데이트 수행**  
     항목의 상태가 변경될 때 솔루션 탐색기의 원본 제어 신호 아이콘을 자동으로 업데이트합니다. 특히 원본 제어에서 솔루션이나 프로젝트를 열 때와 같이 서버를 많이 사용하는 작업을 수행할 때 지연이 발생하면 이 확인란의 선택을 취소하여 성능을 향상시킬 수 있습니다.  
  
     **로그인 ID**  
     소스 제어 공급자에 로그인하는 데 사용할 사용자 이름을 지정합니다. 소스 제어 공급자에서 지원할 경우,이 이름은 채워질에서 자동으로 **로그인** 대화 상자를 원본 제어 서버에 도달 합니다. 이 옵션을 활성화하려면 원본 제어 공급자의 관리자 프로그램을 사용하여 자동 사용자 로그인을 비활성화한 다음 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]를 다시 시작합니다.  
  
     **고급**  
     소스 제어에 항목을 추가하기 위한 추가 옵션을 표시합니다. 이러한 옵션은 원본 제어 공급자에 따라 달라집니다. 이러한 옵션에 대한 도움말은 원본 제어 프로그램에서 제공합니다.  
  
4.  선택 된 **환경** 페이지입니다.  
  
5.  에 **소스 제어 환경 설정** 상자에서 원본 제어 옵션을 설정 하려는 역할을 선택 합니다.  
  
     [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]는 선택한 역할에 대한 기본 원본 제어 옵션을 자동으로 선택합니다. 기본 옵션의 선택을 취소 합니다 **소스 제어 환경 설정** 상자가 표시를 **사용자 지정** 원래 선택된 했던 역할이 사용자 지정을 나타내려면이 옵션을 합니다.  
  
     **소스 제어 환경 설정**  
     사용할 역할을 지정합니다. [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]는 다음 역할을 정의합니다.  
  
    |역할|Description|  
    |----------|-----------------|  
    |**Visual SourceSafe**|가장 일반적으로 사용 되는 설정을 사용 하려는 지정 [!INCLUDE[msCoName](../includes/msconame-md.md)] Visual SourceSafe 사용자입니다.|  
    |**독자적 개발자**|사용자가 독자적으로 작업하도록 지정합니다.|  
    |**Custom**|사용자가 역할에 대한 설정을 수정했음을 나타냅니다.|  
  
     이 역할 중 하나를 선택하면 적절한 원본 제어 옵션이 자동으로 선택됩니다.  
  
     **항목을 체크 인할 때 체크 아웃 유지**  
     소스 제어 저장소를 업데이트하기 위해 항목을 체크 인할 때 사용자에게는 해당 항목이 체크 아웃된 상태로 유지되도록 지정합니다. 특정 체크 인에 대 한이 옵션을 변경 하려면 클릭 합니다 **옵션** 에서 화살표를 **체크** 의 선택을 취소 하 고 대화 상자에서를 **유지 * * * 체크 아웃** 확인란.  
  
     **체크 인 된 항목**  
     체크 아웃되지 않은 항목을 편집하려고 할 때의 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 동작을 지정하는 옵션 목록을 표시합니다. 다음 표에서는 사용할 수 있는 옵션에 대해 설명합니다.  
  
     **저장 하는 중**  
  
    |작업|Description|  
    |------------|-----------------|  
    |**체크 아웃 확인**|표시 된 **체크 아웃** 대화 상자.|  
    |**자동으로 체크 아웃**|표시 하지 않고 항목을 확인 합니다 **체크 아웃** 대화 상자. 이 옵션이 기본 옵션입니다.|  
    |**다른 이름으로 저장**|새 파일로 저장합니다.|  
  
     **편집**  
  
    |작업|Description|  
    |------------|-----------------|  
    |**체크 아웃 확인**|표시 된 **체크 아웃** 대화 상자.|  
    |**단독 체크 아웃 확인**|표시 된 **체크 아웃** 대화 상자.|  
    |**자동으로 체크 아웃**|표시 하지 않고 항목을 확인 합니다 **체크 아웃** 대화 상자. 이 옵션이 기본 옵션입니다.|  
    |**작업 안 함**|파일을 체크 아웃하지 않습니다.|  
  
     **체크 인 한 항목 편집 허용**  
     체크 인한 항목을 메모리에서 편집할 수 있도록 지정합니다. 이 확인란을 선택 하는 경우는 **편집** 단추가 합니다 **체크 아웃** 체크 인 된 항목을 편집 하려고 할 때 대화 상자. 이 단추를 클릭한 후 항목을 편집할 수 있습니다. 항목을 저장하려면 체크 아웃하거나 다른 위치에 저장해야 합니다.  
  
     **다시 설정**  
     소스 제어 환경 대화 상자의 설정을 기본 설정으로 되돌립니다. 예를 들어, 선택한 경우에 **이 대화 상자를 다시 표시 안 함** 원본 제어 대화 상자, 확인란 선택 하는 **재설정** 옵션에 해당 작업이 취소 합니다.  
  
## <a name="see-also"></a>관련 항목  
 [소스 제어 기본 사항](../../2014/database-engine/source-control-basics.md)   
 [원본 제어 연결 변경](../../2014/database-engine/change-source-control-connections.md)   
 [원본 제어에서 파일 제외](../../2014/database-engine/exclude-files-from-source-control.md)  
  
  
