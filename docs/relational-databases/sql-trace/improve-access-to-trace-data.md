---
title: 추적 데이터에 대한 액세스 향상 | Microsoft 문서
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: sql-trace
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Profiler [SQL Server Profiler], space
- SQL Server Profiler, space
- space [SQL Server], SQL Server Profiler
ms.assetid: c260c000-fd53-4831-993f-df6894f3228b
caps.latest.revision: 14
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: ca10030e003582fb02809d65d6034a5cedfb2e02
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32968118"
---
# <a name="improve-access-to-trace-data"></a>추적 데이터에 대한 액세스 향상
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 는 추적 데이터에 대한 액세스를 향상시키기 위해 **temp** 디렉터리의 공간을 사용합니다. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 에는 적어도 10MB의 사용 가능한 공간이 필요합니다. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]를 사용하는 동안 여유 공간이 10MB 이하로 내려가면 모든 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 기능이 중지됩니다.  
  
 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 에서 **temp** 디렉터리의 공간을 사용할 경우 이 공간 사용으로 인해 **temp** 디렉터리가 급격하게 커질 수 있습니다. TEMP 환경 변수의 값을 변경하여 **temp** 디렉터리를 시스템 드라이브가 아닌 드라이브에 두면 파일 증가 문제를 방지할 수 있습니다.  
  
 다음 절차에서는 대부분의 Microsoft Windows 운영 체제에서 TEMP 환경 변수의 값을 변경하는 방법을 설명합니다. 환경 변수를 설정하는 방법은 Windows 운영 체제 설명서를 참조하십시오.  
  
### <a name="to-change-the-temp-environment-variable-in-windows-operating-systems"></a>Windows 운영 체제에서 TEMP 환경 변수를 변경하려면  
  
1.  **시작** 메뉴에서 **제어판**을 선택하고 **시스템**을 클릭합니다.  
  
2.  **시스템 속성** 대화 상자에서 **고급** 탭을 클릭한 다음 **환경 변수**를 클릭합니다.  
  
3.  **시스템 변수**목록을 아래로 스크롤하여 **TEMP** 변수에 해당하는 행을 선택하고 **편집**을 클릭합니다.  
  
4.  **시스템 변수 편집** 대화 상자에서 **temp** 디렉터리를 두려는 드라이브와 디렉터리의 경로 및 이름을 입력합니다.  
  
5.  **확인** 을 클릭하여 변경 내용을 저장합니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server Profiler 시작](../../tools/sql-server-profiler/start-sql-server-profiler.md)   
 [SQL Server 프로파일러](../../tools/sql-server-profiler/sql-server-profiler.md)  
  
  
