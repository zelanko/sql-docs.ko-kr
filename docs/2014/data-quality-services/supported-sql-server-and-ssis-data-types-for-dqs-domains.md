---
title: DQS 도메인에 대해 지원되는 SQL Server 및 SSIS 데이터 형식 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 4931143a-b84d-478b-9b45-174128d36ed3
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 06e593c676c206f863bdb110be5c93e5003b4e13
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "65484097"
---
# <a name="supported-sql-server-and-ssis-data-types-for-dqs-domains"></a>DQS 도메인에 대해 지원되는 SQL Server 및 SSIS 데이터 형식
  SQL Server 및 SQL Server Integration Services(SSIS)에는 여러 가지 데이터 형식이 있지만 DQS 도메인에 대해서는 Date, Decimal, Integer 및 String으로 4개의 데이터 형식이 있습니다. SQL Server 및 SSIS 데이터 형식이 DQS에서 모두 지원되지는 않습니다. 원본 데이터 형식이 DQS에서 지원되고 DQS 도메인 데이터 형식과 일치하는 경우에만 데이터 품질 활동을 수행하기 위해 DQS 도메인에 원본 데이터를 매핑할 수 있습니다. 이 항목에서는 지원되는 SQL Server 및 SSIS 데이터 형식 및 DQS의 4가지 각 도메인 데이터 형식에 대해 매핑할 수 있는 데이터 형식에 대한 정보를 제공합니다.  
  
> [!NOTE]  
>  .xlsx 및 .xls 파일에서는 처음 8개 행에서 가장 많이 사용된 데이터 형식에 의해 원본 열의 데이터 형식이 결정됩니다. 데이터 형식을 따르지 않는 셀에는 null 값이 지정됩니다. 마찬가지로 .csv 파일에서는 처음 8개 행에서 가장 많이 사용된 데이터 형식에 의해 원본 열의 데이터 형식이 결정됩니다.  
  
##  <a name="SQLServer"></a>지원 되는 SQL Server 데이터 형식  
 다음 표에서는 각 DQS 도메인 데이터 형식에 대해 지원되는 SQL Server 데이터 형식에 대한 정보를 제공합니다.  
  
|DQS 도메인 데이터 형식|지원되는 SQL Server 데이터 형식|  
|--------------------------|------------------------------------|  
|Date|date|  
|Decimal|decimal<br /><br /> float<br /><br /> money<br /><br /> numeric<br /><br /> real<br /><br /> smallmoney|  
|정수|bigint<br /><br /> int<br /><br /> smallint<br /><br /> tinyint|  
|String|char<br /><br /> nchar<br /><br /> nvarchar<br /><br /> varchar|  
  
 다른 SQL Server 데이터 형식은 DQS에서 지원되지 않습니다. 모든 SQL Server 데이터 형식에 대한 자세한 내용은 [데이터 형식&#40;Transact-SQL&#41;](/sql/t-sql/data-types/data-types-transact-sql)을 참조하세요.  
  
##  <a name="SSIS"></a>지원 되는 SSIS 데이터 형식  
 다음 표에서는 각 DQS 도메인 데이터 형식에 대해 지원되는 SSIS 데이터 형식에 대한 정보를 제공합니다.  
  
|DQS 도메인 데이터 형식|지원되는 SSIS 데이터 형식|  
|--------------------------|------------------------------|  
|Date|DT_DATE|  
|Decimal|DT_DECIMAL<br /><br /> DT_NUMERIC<br /><br /> DT_R4<br /><br /> DT_R8|  
|정수|DT_I1<br /><br /> DT_I2<br /><br /> DT_I4<br /><br /> DT_I8<br /><br /> DT_U1<br /><br /> DT_U2<br /><br /> DT_U4<br /><br /> DT_U8|  
|String|DT_STR<br /><br /> DT_WSTR|  
  
 다른 SSIS 데이터 형식은 DQS에서 지원되지 않습니다. 모든 SSIS 데이터 형식에 대한 자세한 내용은 [Integration Services Data Types](../integration-services/data-flow/integration-services-data-types.md)을 참조하십시오.  
  
## <a name="see-also"></a>참고 항목  
 [도메인 관리](../../2014/data-quality-services/managing-a-domain.md)  
  
  
