---
title: 서버 속성(연결 페이지) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.swb.serverproperties.connections.f1
ms.assetid: 33be8ac5-12dd-4b8a-99e0-68261c219dd2
caps.latest.revision: 26
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: c57ebc36fa8a8145ee1212341e74d07c8d1b1522
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36187264"
---
# <a name="server-properties-connections-page"></a>서버 속성(연결 페이지)
  이 페이지를 사용하여 연결 옵션을 확인하거나 수정할 수 있습니다.  
  
## <a name="connections"></a>Connections  
 **최대 동시 연결 수(0 = 제한 없음)**  
 이 값을 0이 아닌 값으로 설정하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 허용하는 연결 수가 제한됩니다.  
  
> [!CAUTION]  
>  이 값을 1이나 2와 같은 작은 값으로 설정하면 관리자가 서버를 관리하기 위해 연결하지 못할 수도 있습니다. 하지만 관리자 전용 연결을 통한 연결은 언제든지 가능합니다.  
  
## <a name="default-connection-options"></a>기본 연결 옵션  
 **Default connection options**  
 다음 표에서 설명하는 기본 연결 옵션을 지정합니다.  
  
|구성 옵션|Description|  
|--------------------------|-----------------|  
|**지연된 제약 조건 검사 비활성화**|중간 또는 지연된 제약 조건 검사를 제어합니다.|  
|**암시적 트랜잭션**|문 실행 시 트랜잭션을 암시적으로 실행할지 여부를 제어합니다.|  
|**커밋 시 커서 닫기**|커밋 작업 수행 후 커서의 동작을 제어합니다.|  
|**ANSI 경고**|집계 경고의 잘림과 NULL을 제어합니다.|  
|**ANSI 패딩**|고정 길이 변수의 패딩을 제어합니다.|  
|**ANSI NULL**|등호 연산자 사용 시 `NULL` 처리를 제어합니다.|  
|**산술 연산 중단**|쿼리 실행 중 오버플로 또는 0으로 나누기 오류가 발생하면 쿼리를 종료합니다.|  
|**산술 연산 무시**|쿼리 실행 중 오버플로 또는 0으로 나누기 오류가 발생하면 NULL을 반환합니다.|  
|**따옴표 붙은 식별자**|식을 평가할 때 큰따옴표와 작은따옴표를 구분합니다.|  
|**열 개수 표시 안 함**|영향 받는 행 수를 지정하는 각 문의 끝에 반환되는 메시지를 해제합니다.|  
|**ANSI NULL 기본값 설정**|세션에서 Null 허용에 대해 ANSI 호환성을 사용할 때 경고합니다. 명시적 Null 허용 없이 정의된 새 열은 Null을 허용하도록 정의됩니다.|  
|**ANSI NULL 기본값 해제**|세션이 null 허용에 대해 ANSI 호환성을 사용하지 않을 때 경고합니다. 명시적 Null 허용 없이 정의된 새 열은 Null을 허용하지 않도록 정의됩니다.|  
|**Null 연결 시 Null 생성**|문자열이 있는 NULL 값을 연결할 때 NULL을 반환합니다.|  
|**숫자 반올림 시 중단**|식의 전체 자릿수가 떨어지면 오류가 발생합니다.|  
|**트랜잭션 중단**|Transact-SQL 문이 런타임 오류를 일으키면 트랜잭션을 롤백합니다.|  
  
 연결 옵션에 대한 자세한 내용을 보려면 온라인 설명서에서 해당 옵션을 검색하십시오.  
  
## <a name="remote-server-connections"></a>원격 서버 연결  
 **이 서버에 대한 원격 연결 허용**  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스를 실행하는 원격 서버에서의 저장 프로시저 실행을 제어합니다. 이 확인란을 선택하는 것은 **sp_configure remote access** 옵션을 1로 설정하는 것과 같습니다. 확인란의 선택을 취소하면 원격 서버에서 저장 프로시저를 실행할 수 없습니다.  
  
 **원격 쿼리 제한 시간(초, 0 = 제한 시간 없음)**  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 제한 시간이 초과될 때까지 원격 작업을 수행할 수 있는 시간을 초 단위로 지정합니다. 기본값은 600이며 10분 대기할 수 있습니다.  
  
 **서버 간 통신에 분산 트랜잭션 필요**  
 MS DTC( [!INCLUDE[msCoName](../../includes/msconame-md.md)] Distributed Transaction Coordinator) 트랜잭션을 통해 서버 간 프로시저 동작을 보호합니다. 자세한 내용은 [Configure the remote proc trans Server Configuration Option](configure-the-remote-proc-trans-server-configuration-option.md)을 참조하세요.  
  
## <a name="property-page-display-options"></a>속성 페이지 표시 옵션  
 **구성 값**  
 이 창의 옵션에 대해 구성된 값을 표시합니다. 이러한 값을 변경한 후에는 **실행 값** 을 클릭하여 변경 사항이 적용되었는지 여부를 확인합니다. 변경 사항이 적용되지 않은 경우 먼저 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스를 다시 시작해야 합니다.  
  
 **실행 값**  
 이 창의 옵션에 대한 현재 실행 값을 볼 수 있습니다. 이 값은 읽기 전용입니다.  
  
## <a name="see-also"></a>관련 항목  
 [옵션 &#40;쿼리 실행: SQL Server: 고급 페이지&#41;](../options-query-execution-sql-server-advanced-page.md)   
 [서버 구성 옵션&#40;SQL Server&#41;](server-configuration-options-sql-server.md)  
  
  