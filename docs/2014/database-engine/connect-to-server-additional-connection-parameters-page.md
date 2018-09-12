---
title: 서버에 연결(추가 연결 매개 변수 페이지) | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.swb.connecttoserver.options.registeredservers.f1
ms.assetid: ba34b01a-6289-4eb8-8341-fa3d9ec87b3f
caps.latest.revision: 11
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 238a558f7b11c122012c2bfbe9538fa803fa8444
ms.sourcegitcommit: 8ae6e6618a7e9186aab3c6a37ea43776aa9a382b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/06/2018
ms.locfileid: "43816259"
---
# <a name="connect-to-server-additional-connection-parameters-page"></a>서버에 연결(추가 연결 매개 변수 페이지)
  **의** 연결 대상 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 대화 상자에서는 가장 일반적인 연결 문자열 값을 옵션으로 제공합니다. **추가 연결 매개 변수** 페이지를 사용하면 연결 문자열에 연결 매개 변수를 더 추가할 수 있습니다.  
  
-   모든 ODBC 연결 매개 변수를 추가 연결 매개 변수로 사용할 수 있습니다.  
  
-   추가 연결 매개 변수는 **;parameter1=value1;parameter2=value2**형식으로 추가해야 합니다.  
  
-   **추가 연결 매개 변수** 페이지를 사용하여 추가한 매개 변수는 **연결 대상** 대화 상자 옵션을 사용하여 선택한 매개 변수에 추가됩니다.  
  
-   제공된 각 매개 변수의 마지막 인스턴스는 매개 변수의 이전 인스턴스보다 우선합니다. **추가 연결 매개 변수** 페이지를 사용하여 추가한 매개 변수가 그 다음이고 **로그인** 또는 **연결 속성** 탭의 매개 변수를 대체합니다. 예를 들어 **로그인** 탭에서 **서버 이름** 이 **SERVER1**이고 **추가 연결 매개 변수** 페이지에 **;SERVER=SERVER2**가 있으면 **SERVER2**에 연결됩니다.  
  
-   **추가 연결 매개 변수** 페이지를 사용하여 추가한 매개 변수는 항상 일반 텍스트로 전달됩니다.  
  
    > [!IMPORTANT]  
    >  **추가 연결 매개 변수** 페이지에 로그인 자격 증명과 암호를 포함하지 마십시오. 이러한 정보는 네트워크로 전달될 때 암호화되지 않습니다. 대신 **로그인** 탭을 사용하십시오.  
  
## <a name="task-list"></a>작업 목록  
  
### <a name="to-show-the-additional-connection-parameters-page"></a>추가 연결 매개 변수 페이지를 표시하려면  
  
1.  [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)]의 **쿼리** 메뉴에서 **연결**을 가리킨 다음 **연결**을 클릭합니다.  
  
2.  **연결 대상** 대화 상자에서 **옵션**을 클릭하고 **추가 연결 매개 변수** 탭을 클릭합니다.  
  
## <a name="examples"></a>예  
  
### <a name="example-a-connecting-to-the-database-engine"></a>예 1: 데이터베이스 엔진에 연결  
 ACCOUNTING 서버의 [!INCLUDE[ssSampleDBnormal](../includes/sssampledbnormal-md.md)] 데이터베이스에 연결하려면 **추가 연결 매개 변수** 페이지에 다음을 입력합니다.  
  
```  
;SERVER=ACCOUNTING;DATABASE=AdventureWorks2012  
```  
  
### <a name="example-b-connecting-to-analysis-services"></a>예 2: Analysis Services에 연결  
 Analysis Servers에 연결하여 알림을 수신하는 모든 파티션이 실시간으로 쿼리(캐싱 우회)되도록 하고 쓰기 저장(writeback) 제한 시간 값을 5로 설정하려면 **추가 연결 매개 변수** 페이지에 다음을 입력합니다.  
  
```  
;Real Time Olap=TRUE;Writeback Timeout=5  
```  
  
  
