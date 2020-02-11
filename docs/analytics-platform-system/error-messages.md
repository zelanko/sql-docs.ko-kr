---
title: 오류 메시지
description: PDW (병렬 데이터 웨어하우스) 오류 메시지는 PDW 구성 요소에서 발생 하는 오류 및 문제를 보고 하 고 PDW를 통해 표시 되는 SQL Server 오류가 포함 될 수도 있습니다. 이러한 오류 메시지에는 정보를 표시 하기 위해 일관 된 구문이 사용 됩니다. 이 구문을 이해 하면 문제를 식별 하 고 해결할 수 있습니다.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 2d89e80a89df53e85ef8d2bf53c369d9e4dc0d49
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "74401159"
---
# <a name="error-messages-in-parallel-data-warehouse"></a>병렬 데이터 웨어하우스의 오류 메시지

PDW (병렬 데이터 웨어하우스) 오류 메시지는 PDW 구성 요소에서 발생 하는 오류 및 문제를 보고 하 고 PDW를 통해 표시 되는 SQL Server 오류가 포함 될 수도 있습니다. 이러한 오류 메시지에는 정보를 표시 하기 위해 일관 된 구문이 사용 됩니다. 이 구문을 이해 하면 SQL Server PDW에 대 한 문제를 식별 하 고 해결할 수 있습니다.  
  
## <a name="Basics"></a>오류 메시지의 기본 사항  
반환 되는 오류 메시지는 동일한 구문을 따릅니다.  
  
`Error_Indicator [SQL_State_Code] [Driver_Details] [QueryID] Message_String`  
  
각 필드에 대 한 가능한 값은 다음과 같습니다.  
  
|필드|Description|예제|  
|---------|---------------|-----------|  
|*Error_Indicator*|문제에 대해 사용자에 게 경고 하는 "오류" 또는 기타 텍스트입니다.|오류|  
|*SQL_State_Code*|ODBC 사양에 따른 SQL 상태 코드입니다. 드라이버는 응용 프로그램에 메시지를 반환할 때마다 적절 한 SQL 상태 코드를 생성 합니다. "Microsoft" 텍스트는 오류의 원인을 나타냅니다.|42000|  
|*Driver_Details*|사용 되는 드라이버 유형에 해당 하는 드라이버 종속 세부 정보입니다.|ODBC SQL Server 2008 R2 병렬 데이터 웨어하우스 드라이버|  
|*QueryID*|쿼리의 고유 식별자입니다. 이 값을 사용 하 여 쿼리 처리와 관련 된 추가 정보를 찾을 수 있습니다. 예를 들어 쿼리 실행 세부 정보는 쿼리 ID를 사용 하 여 관리 콘솔에서 찾을 수 있습니다. 자세한 내용은 [관리자 콘솔을 사용 하 여 어플라이언스 모니터링](monitor-the-appliance-by-using-the-admin-console.md)을 참조 하세요.<br /><br />QueryID을 적용할 수 없는 경우 사용자에 게 "내부" 텍스트가 반환 됩니다.|QID2377|  
|*Message_String*|사람이 읽을 수 있는 오류 또는 문제에 대 한 설명입니다. SQL Server 오류를 반환할 때 SQL Server 메시지 텍스트입니다.|UPDATE 문의 set 목록에는 같은 할당만 표시할 수 있습니다.|  
  
이러한 예제 값은 다음과 같이 사용자에 게 제공 됩니다.  
  
`ERROR [42000] [Microsoft][ODBC SQL Server 2008 R2 Parallel Data Warehouse driver][QID2380]Only equal assignment can appear in the set list of an UPDATE statement.`  
  
## <a name="see-also"></a>참고 항목  
<!-- MISSING LINKS 
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  
-->
[관리 콘솔 경고 이해](understanding-admin-console-alerts.md)  
  
