---
title: 오류 메시지-병렬 데이터 웨어하우스 | Microsoft Docs
description: 오류를 보고 하는 병렬 데이터 웨어하우스 (PDW) 오류 메시지 및 PDW 구성 요소에서 발생 한 문제와 PDW를 통해 표시 되는 SQL Server 오류를 포함할 수도 있습니다. 이러한 오류 메시지는 정보를 제공 하는 것에 대 한 일관성 있는 구문을 사용 합니다. 이 구문을 이해 하면를 식별 하 여 문제를 해결 합니다.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 3ffc7a097845f4652f56d82c572ecfab868d33f1
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63042599"
---
# <a name="error-messages-in-parallel-data-warehouse"></a>병렬 데이터 웨어하우스에서 오류 메시지

오류를 보고 하는 병렬 데이터 웨어하우스 (PDW) 오류 메시지 및 PDW 구성 요소에서 발생 한 문제와 PDW를 통해 표시 되는 SQL Server 오류를 포함할 수도 있습니다. 이러한 오류 메시지는 정보를 제공 하는 것에 대 한 일관성 있는 구문을 사용 합니다. 이 구문을 이해 하면를 식별 하 여 SQL Server PDW에서 문제를 해결 합니다.  
  
## <a name="Basics"></a>오류 메시지 기본 사항  
반환 되는 오류 메시지는 동일한 구문을 따릅니다.  
  
`Error_Indicator [SQL_State_Code] [Driver_Details] [QueryID] Message_String`  
  
다음은 각 필드에 대 한 잠재적인 값입니다.  
  
|필드|Description|예제|  
|---------|---------------|-----------|  
|*Error_Indicator*|"오류" 단어 또는 문제가 사용자에 게 알리는 다른 텍스트입니다.|ERROR|  
|*SQL_State_Code*|ODBC 사양에 따라 표시 되는 SQL 상태 코드입니다. 드라이버는 응용 프로그램에 메시지를 반환 하는 언제 든 지 적절 한 SQL 상태 코드를 생성 합니다. "Microsoft" 텍스트에는 오류 원인을 나타냅니다.|42000|  
|*Driver_Details*|드라이버에 따라 다릅니다 등 세부 정보 사용 되는 드라이버의 형식입니다.|ODBC SQL Server 2008 R2 병렬 데이터 웨어하우스 드라이버|  
|*QueryID*|쿼리에 대 한 고유 식별자입니다. 쿼리 처리와 관련 된 추가 정보를 찾으려면이 값을 사용 합니다. 예를 들어, 쿼리 실행 정보를 찾을 수 있습니다 관리 콘솔에서 쿼리 id입니다. 자세한 내용은 [관리자 콘솔을 사용 하 여 어플라이언스 모니터링](monitor-the-appliance-by-using-the-admin-console.md)합니다.<br /><br />QueryID는 적용할 수 없는 경우 "내부" 텍스트는 사용자에 게 반환 됩니다.|QID2377|  
|*Message_String*|오류 또는 문제를 알기 쉬운 설명입니다. SQL Server 오류를 반환 하는 경우 SQL Server 메시지 텍스트입니다.|같은 할당만 UPDATE 문의 set 목록에 나타날 수 있습니다.|  
  
다음 예제에서는 값 같이 사용자에 게 표시 됩니다.  
  
`ERROR [42000] [Microsoft][ODBC SQL Server 2008 R2 Parallel Data Warehouse driver][QID2380]Only equal assignment can appear in the set list of an UPDATE statement.`  
  
## <a name="see-also"></a>관련 항목  
<!-- MISSING LINKS 
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  
-->
[관리 콘솔 경고 이해](understanding-admin-console-alerts.md)  
  
