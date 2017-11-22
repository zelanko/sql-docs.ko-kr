---
title: "오류 메시지 (SQL Server PDW)"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.prod: sql-non-specified
ms.prod_service: mpp-data-warehouse
ms.service: 
ms.component: analytics-platform-system
ms.technology: mpp-data-warehouse
ms.custom: 
ms.date: 01/13/2017
ms.reviewer: na
ms.suite: sql
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e6223cba-2dec-4b8a-bc10-e2ef6a821fe0
caps.latest.revision: "9"
ms.openlocfilehash: 7c7d453bc2ac68db724734d7db7cf58e35611ba8
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="error-messages"></a>오류 메시지
SQL Server PDW 오류 메시지는 오류 보고와 문제는 SQL Server PDW 구성 요소에서 발생 하 고 SQL Server PDW를 통해 표시 되는 SQL Server 오류에 포함 될 수도 있습니다. 이러한 오류 메시지는 정보를 표시 하기 위한 일관성 있는 구문을 사용 합니다. 이 구문을 이해 하면 파악 하 고 SQL Server PDW에서 문제를 해결할 수 있습니다.  
  
## <a name="Basics"></a>오류 메시지의 기본 사항  
반환 되는 오류 메시지에는 동일한 구문을 따릅니다.  
  
`Error_Indicator [SQL_State_Code] [Driver_Details] [QueryID] Message_String`  
  
다음은 각 필드에 대 한 잠재적인 값입니다.  
  
|필드|Description|예제|  
|---------|---------------|-----------|  
|*Error_Indicator*|"오류" 단어 또는 문제를 사용자에 게 알리는 기타 텍스트입니다.|ERROR|  
|*SQL_State_Code*|ODBC 사양에 따라 표시 되는 SQL 상태 코드입니다. 드라이버는 응용 프로그램에 메시지를 반환 하는 언제 든 지 적절 한 SQL 상태 코드를 생성 합니다. "Microsoft" 텍스트에는 오류의 원인을 나타냅니다.|42000|  
|*Driver_Details*|사용 되는 드라이버의 형식 등의 종속 드라이버 정보|ODBC SQL Server 2008 R2 병렬 데이터 웨어하우스 드라이버|  
|*QueryID*|쿼리에 대 한 고유 식별자입니다. 이 값을 사용 하 여 쿼리 처리와 관련 된 추가 정보를 찾을 수입니다. 예를 들어 쿼리 실행 세부 정보에서에서 찾을 수 있습니다 관리 콘솔 쿼리 ID를 사용 하 여 자세한 내용은 참조 [관리 콘솔을 사용 하 여 어플라이언스에 모니터링](monitor-the-appliance-by-using-the-admin-console.md)합니다.<br /><br />QueryID는 적용할 수 없는 경우 "내부" 텍스트는 사용자에 게 반환 됩니다.|QID2377|  
|*Message_String*|오류 또는 문제 이해 하기 쉬운 설명입니다. SQL Server 오류를 반환할 때 SQL Server 메시지 텍스트입니다.|같은 할당만 UPDATE 문의 set 목록에 나타날 수 있습니다.|  
  
이러한 예제에서는 값은 다음과 같이 사용자에 게 표시할:  
  
`ERROR [42000] [Microsoft][ODBC SQL Server 2008 R2 Parallel Data Warehouse driver][QID2380]Only equal assignment can appear in the set list of an UPDATE statement.`  
  
## <a name="see-also"></a>관련 항목:  
<!-- MISSING LINKS 
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  
-->
[관리 콘솔 경고 이해](understanding-admin-console-alerts.md)  
  
