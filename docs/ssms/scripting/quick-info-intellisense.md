---
title: 요약 정보(IntelliSense)
description: IntelliSense 요약 정보 옵션을 사용하여 코드의 모든 식별자에 대한 완전한 선언을 표시하는 방법을 알아봅니다. SQL Server Management Studio에서 이 옵션은 데이터베이스 엔진 편집기 및 XML 쿼리 편집기에서 사용할 수 있습니다.
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.technology: ssms
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- Quick Info option [IntelliSense]
- declarations [IntelliSense]
- IntelliSense [SQL Server], Quick Info
- identifier declarations [IntelliSense]
ms.assetid: 3c8b59f4-1922-4bde-844f-5f2306514d96
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 7edb6d72433eed80464c563219aa1840fdf2f918
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97466344"
---
# <a name="quick-info-intellisense"></a>요약 정보(IntelliSense)
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] IntelliSense **요약 정보** 옵션은 코드의 모든 식별자에 대한 완전한 선언을 표시합니다. 마우스 포인터를 식별자 위로 이동하면 노란색 팝업 창에 해당 선언이 표시됩니다. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 **요약 정보** 는 데이터베이스 엔진 및 XML 쿼리 편집기에서 사용할 수 있습니다.  
  
## <a name="transact-sql-quick-info"></a>Transact-SQL 요약 정보  
 **쿼리 편집기의** 요약 정보 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 에는 두 가지 유형의 정보가 표시됩니다. 디버그 모드가 아닐 때는 **요약 정보** 에 식 선언이 표시됩니다. 디버그 모드일 때는 **요약 정보** 에 식 이름과 식의 현재 값이 표시됩니다.  
  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 쿼리 편집기에서 IntelliSense에서 지원하는 **구문의 이러한 부분에 대해서만** 요약 정보 [!INCLUDE[tsql](../../includes/tsql-md.md)] 를 사용할 수 있습니다. 예를 들어 IntelliSense에서 지원하지 않는 데이터 형식이 있는 개체에 대한 식별자 위로 마우스 포인터를 이동하면 **요약 정보** 팝업 창에 데이터 형식이 지원되지 않는다는 메시지가 포함됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [IntelliSense에서 지원되는 Transact-SQL 구문](./transact-sql-syntax-supported-by-intellisense.md)  
  
