---
title: 소스 제어 연결 변경 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- connections [SQL Server Management Studio], source controls
- source controls [SQL Server Management Studio], connections
ms.assetid: 538e3beb-f99c-4095-bd65-6413e872d26e
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: d57f5938cb888a955645f5a9e0b01eeacfc1142b
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62812792"
---
# <a name="change-source-control-connections"></a>원본 제어 연결 변경
  소스 제어에서 솔루션을 처음 추가하거나 열면 원본 제어 공급자는 로컬 솔루션 디렉터리의 루트 폴더와 해당 서버 폴더 간에 연결을 설정합니다.  
  
 루트 폴더(통합 루트라고도 함)는 클라이언트에 상주합니다. 루트 폴더는 솔루션이나 프로젝트가 참조하는 모든 파일을 그 아래에서 찾을 수 있는 폴더입니다. 최신 버전의 솔루션, 기록 및 상태 정보를 찾으려면 소스 제어 서버에 상주하는 서버 폴더를 찾습니다. [!INCLUDE[msCoName](../includes/msconame-md.md)] Visual SourceSafe에서는 서버 폴더를 프로젝트라고 합니다.  
  
 대부분의 상황에서는 해당 서버 폴더에서 솔루션을 언바인딩하거나 솔루션 연결을 끊어야 합니다. 예를 들어 소스 제어 공급자가 상주하는 컴퓨터를 사용할 수 없는 경우 백업 컴퓨터에 연결하여 솔루션을 백업된 서버 폴더에 다시 바인딩하고 작업을 정상적으로 재개할 수 있습니다. 또한 소스 제어 프로젝트가 분기된 경우 새 프로젝트 버전이 상주하는 서버 폴더에 솔루션을 바인딩해야 할 수 있습니다.  
  
 소스 제어 공급자의 사용자 인터페이스를 사용하여 솔루션이 바인딩되는 서버 폴더를 변경할 수 있습니다. [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 환경 내에서 소스 제어 사용자 인터페이스를 열 수 있습니다.  
  
#### <a name="to-open-the-source-control-user-interface-from-the-studio-environment"></a>Studio 환경에서 소스 제어 사용자 인터페이스를 열려면  
  
1.  에 **파일** 메뉴에서 **소스 제어**를 클릭 하 고 **Microsoft Visual SourceSafe 시작**합니다.  
  
## <a name="see-also"></a>관련 항목  
 [소스 제어 기본 사항](../../2014/database-engine/source-control-basics.md)   
 [원본 제어 옵션 설정](../../2014/database-engine/set-source-control-options.md)   
 [원본 제어에서 파일 제외](../../2014/database-engine/exclude-files-from-source-control.md)  
  
  
