---
description: SSMS 사용 현황 및 진단 데이터 수집에 대한 로컬 감사
title: 사용량 현황 및 진단 데이터
ms.custom: seo-lt-2019
ms.date: 04/16/2019
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
ms.assetid: c28ffa44-7b8b-4efa-b755-c7a3b1c11ce4
author: markingmyname
ms.author: maghan
ms.openlocfilehash: c26ab977839927751903eead0533256ab91fde2c
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88370139"
---
# <a name="local-audit-for-ssms-usage-and-diagnostic-data-collection"></a>SSMS 사용 현황 및 진단 데이터 수집에 대한 로컬 감사
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

SSMS(SQL Server Management Studio)에는 익명 기능 사용 현황 및 진단 데이터를 수집하고 Microsoft에 보낼 수 있는 인터넷 사용 기능이 포함되어 있습니다. SSMS는 표준 컴퓨터 정보 및 Microsoft로 전송되어 SSMS의 품질, 보안 및 안정성 개선의 목적으로 분석될 수 있는 사용 및 성능에 대한 정보를 수집할 수 있습니다. 사용자 이름, 주소 또는 기타 개인 정보는 수집하지 않습니다. 자세한 내용은 [Microsoft 개인정보처리방침](https://privacy.microsoft.com/privacystatement) 및 [SQL Server 개인 정보 제공](https://go.microsoft.com/fwlink/?LinkID=868444)을 참조하세요.

## <a name="audit-feature-usage-and-diagnostic-data"></a>감사 기능 사용 및 진단 데이터

SSMS를 통해 수집된 기능 사용량 현황 데이터를 확인하려면 다음 단계를 수행합니다.

1.  SSMS를 시작합니다.
2.  **보기**를 클릭하고 기본 메뉴에서 **출력**을 클릭하여 **출력** 창을 표시합니다. 
3.  **출력** 창이 표시되면 **출력 보기 선택:** 메뉴에서 **원격 분석**을 선택합니다.

SSMS를 통해 데이터베이스와 상호 작용할 경우 **출력** 창에 수집된 데이터가 표시됩니다.

## <a name="enable-or-disable-usage-and-diagnostic-data-collection-in-ssms"></a>SSMS에서 사용 현황 및 진단 데이터 수집 사용 또는 사용 안 함

SSMS 사용량 현황 데이터 수집에 참여하거나 참여하지 않으려면 다음을 수행합니다.

- SQL Server Management Studio 17:

  `Subkey = HKEY_CURRENT_USER\Software\Microsoft\SQL Server Management Studio\14.0`

  레지스트리 항목 이름 = `UserFeedbackOptIn`

  항목 유형 `DWORD`: `0`은 참여하지 않음, `1`은 참여함

  또한 SSMS 17.x는 Visual Studio 2015 셸에 기반을 두고 있으며, Visual Studio를 설치하면 기본적으로 고객 피드백이 활성화됩니다.  

  개별 컴퓨터에서 고객 피드백을 비활성화하도록 Visual Studio를 구성하려면 다음 레지스트리 하위 키 값(`0`)을 문자열 `HKEY_LOCAL_MACHINE\Software\Policies\Microsoft\VisualStudio\SQM OptIn`으로 변경합니다.

  예를 들어 하위 키를 다음으로 변경합니다.  
  `HKEY_LOCAL_MACHINE\Software\Policies\Microsoft\VisualStudio\SQM OptIn `=` 0`

  이러한 레지스트리 하위 키에 대한 레지스트리 기반 그룹 정책은 SQL Server 2017 사용 현황 및 진단 데이터 수집에 따라 적용됩니다.

- SQL Server Management Studio 18:

  `Subkey = HKEY_CURRENT_USER\Software\Microsoft\SQL Server Management Studio\18.0_IsoShell`

  레지스트리 항목 이름 = `UserFeedbackOptIn`

  항목 유형 `DWORD`: `0`은 참여하지 않음, `1`은 참여함

## <a name="see-also"></a>참조

- [SQL Server 사용 현황 및 진단 데이터 수집 구성](../sql-server/usage-and-diagnostic-data-configuration-for-sql-server.md)
- [SQL Server 사용 현황 및 진단 데이터 수집에 대한 로컬 감사](https://msdn.microsoft.com/library/mt743085.aspx)
