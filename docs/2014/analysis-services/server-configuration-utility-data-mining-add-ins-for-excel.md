---
title: 서버 구성 유틸리티 (데이터 마이닝 추가 기능 Excel 용) | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 28435f86-5cec-4a1e-9b7d-b2069c1ddddb
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: bdc8434673d9220f22d31f1736bd67012653dc88
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66069067"
---
# <a name="server-configuration-utility-data-mining-add-ins-for-excel"></a>서버 구성 유틸리티(Excel용 데이터 마이닝 추가 기능)
  Excel 용 데이터 마이닝 추가 기능을 설치할 때 서버 구성 유틸리티도 설치 되어 및 추가 기능을 열면 처음으로 실행 됩니다. 이 항목에서는 유틸리티를 사용 하 여 인스턴스에 연결 하는 방법을 설명 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 및 데이터 마이닝 모델을 사용 하 여 작업에 사용할 데이터베이스를 설정 합니다.  
  

  
##  <a name="bkmk_step1"></a> 1단계: Analysis Services에 연결  
 데이터 마이닝 알고리즘을 제공하고 사용자의 데이터 마이닝 모델을 저장하는 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 서버를 선택합니다.  
  
 데이터 마이닝을 설정하기 위한 연결을 만들 때는 데이터 마이닝 모델을 실험할 수 있는 서버를 선택해야 합니다. 서버에서 새 데이터베이스를 만들고 이를 데이터 마이닝 전용으로 사용하거나 관리자에게 데이터 마이닝 서버를 준비하도록 요청하는 것이 좋습니다. 이렇게 하면 다른 서비스의 성능에 영향을 주지 않고 모델을 구축할 수 있습니다.  
  
 데이터 마이닝에 사용하는 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 서버는 원본 데이터와 동일한 서버에 있을 필요가 없습니다.  
  
 **서버 이름**  
 데이터 마이닝에 사용할 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 인스턴스가 포함된 서버의 이름을 입력합니다.  
  
 **인증**  
 인증 방법을 지정합니다. 관리자가 HTTPPump를 통해 서버에 액세스하도록 구성하지 않은 한 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]에 연결하려면 Windows 인증이 필요합니다.  
  
##  <a name="bkmk_step2"></a> 2단계: 임시 모델 허용  
 추가 기능을 사용하려면 먼저 임시 마이닝 모델 생성을 허용하도록 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 서버 속성을 변경해야 합니다.  
  
 임시 마이닝 모델 이라고 *세션 모델*합니다. 현재 세션이 열려 있는 동안에만 모델이 저장되기 때문입니다. 서버에 대한 연결을 닫으면 세션이 종료되고 세션이 열려 있는 동안 사용된 모든 모델이 삭제됩니다.  
  
 세션 마이닝 모델을 사용하더라도 서버의 스토리지 공간에는 영향이 없지만 데이터 마이닝 모델을 만드는 데 따르는 오버헤드가 서버 성능에 영향을 줄 수 있습니다.  
  
 마법사는 먼저 사용자가 지정한 서버에서 설정을 검색합니다. 서버에서 이미 임시 마이닝 모델을 허용 하는 경우 클릭할 수 있습니다 **다음** 계속 합니다. 마법사에는 또한 지정된 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 서버에서 임시 마이닝 모델을 사용하도록 설정하는 방법 또는 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 관리자에게 요청을 수행하는 방법에 대한 지침이 제공됩니다.  
  
##  <a name="bkmk_step3"></a> 3단계: 추가 기능 사용자 용 데이터베이스 만들기  
 설정 및 구성 마법사의 이 페이지에서 데이터 마이닝 전용의 새 데이터베이스를 만들거나 기존 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 데이터베이스를 선택할 수 있습니다.  
  
> [!WARNING]  
>  데이터 마이닝을 위해서는 다차원 모드로 실행 중인 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 인스턴스가 필요합니다. 테이블 형식 모드에서는 데이터 마이닝이 지원되지 않습니다.  
  
 데이터 마이닝 전용의 별도의 데이터베이스를 만드는 것이 좋습니다. 이렇게 하면 다른 솔루션 개체에 영향을 주지 않고 데이터 마이닝 모델을 실험할 수 있습니다.  
  
 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 인스턴스에서 기존 데이터베이스를 선택할 경우에는, 추가 기능을 사용해서 모델을 만들 때 해당 이름의 모델이 이미 있으면 기존 모델을 덮어쓸 수 있으므로 주의해야 합니다.  
  
 **새 데이터베이스 만들기**  
 선택한 서버에 새 데이터베이스를 만들려면 이 옵션을 선택합니다. 데이터 마이닝 데이터베이스에는 데이터 원본, 마이닝 구조 및 마이닝 모델이 저장됩니다.  
  
 **데이터베이스 이름**  
 새 데이터베이스의 이름을 입력합니다. 이름이 사용 중이 아니면 해당 이름으로 데이터베이스가 만들어집니다.  
  
 **기존 데이터베이스 사용**  
 기존 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 데이터베이스를 사용하려면 이 옵션을 선택합니다.  
  
 **데이터베이스 백업**  
 기존 데이터베이스를 사용하는 옵션을 선택한 경우 목록에서 데이터베이스 이름을 선택해야 합니다.  
  
##  <a name="bkmk_step4"></a> 4 단계: 추가 기능 사용자에 게 적절 한 권한 부여  
 사용자(및 추가 기능의 다른 모든 사용자)에게 데이터 마이닝 구조 및 모델을 탐색, 편집, 처리 또는 생성하는 데 필요한 권한이 있는지 확인해야 합니다.  
  
 기본적으로 추가 기능을 사용하려면 통합 Windows 인증이 필요합니다.  
  
 **추가 기능 사용자에 게 데이터베이스 관리 권한 부여**  
 나열된 사용자에게 데이터베이스에 대한 관리 액세스 권한을 부여하려면 이 옵션을 선택합니다.  
  
> [!NOTE]  
>  이러한 권한은에 나열 된 데이터베이스에만 적용 합니다 **데이터베이스 이름** 상자입니다.  
  
 **데이터베이스 이름**  
 선택한 데이터베이스의 이름을 표시합니다.  
  
 **추가할 사용자 또는 그룹 지정**  
 데이터 마이닝에 사용되는 데이터베이스에 대한 액세스 권한을 가질 로그인을 선택합니다.  
  
 **추가**  
 대화 상자를 열어 사용자 또는 그룹을 추가하려면 클릭합니다.  
  
 **제거**  
 선택한 사용자 또는 그룹을 관리 권한이 있는 사용자 목록에서 제거하려면 클릭합니다.  
  
  
