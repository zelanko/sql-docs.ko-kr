---
title: "로컬 계산 컨텍스트 (SQL과 R 심층 분석)에서 데이터를 분석 | Microsoft Docs"
ms.date: 12/18/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: 
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: tutorial
applies_to:
- SQL Server 2016
- SQL Server 2017
dev_langs: R
ms.assetid: 787bb526-4a13-40fa-9343-75d3bf5ba6a2
caps.latest.revision: "13"
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: Inactive
ms.openlocfilehash: 0705d7253979dd5b688a0ca5f78720304a368e3d
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/08/2018
---
# <a name="analyze-data-in-local-compute-context-sql-and-r-deep-dive"></a>로컬 계산 컨텍스트 (SQL과 R 심층 분석)에서 데이터 분석

이 문서는 데이터 과학 심층 분석 자습서를 사용 하는 방법에 대 한 일부 [RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) SQL Server와 함께 합니다.

이 섹션에서는 로컬 계산 컨텍스트로 다시 전환 하 고 성능을 최적화 하기 위해 컨텍스트 간에 데이터를 이동 하는 방법을 설명 합니다.

I 수는 있지만 더 빠르게 서버 컨텍스트를 사용 하 여 복잡 한 R 코드를 실행 하려면, 때로는 것이 더 편리의 데이터를 가져오는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로컬 워크스테이션에서 분석 하 고 있습니다.

## <a name="create-a-local-summary"></a>로컬 요약 만들기

1. 모든 작업을 로컬에서 수행하도록 계산 컨텍스트를 변경합니다.
  
    ```R
    rxSetComputeContext ("local")
    ```
  
2. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 데이터를 추출하는 경우 각 읽기에서 추출되는 행 수를 늘리면 대체로 성능이 향상됩니다.  이렇게 하려면 데이터 원본에 대한 *rowsPerRead* 매개 변수의 값을 늘립니다. 이전에는 *rowsPerRead* 값이 5000으로 설정되었습니다.
  
    ```R
    sqlServerDS1 <- RxSqlServerData(
       connectionString = sqlConnString,
       table = sqlFraudTable,
       colInfo = ccColInfo,
       rowsPerRead = 10000)
    ```

3. 호출 **rxSummary** 새 데이터 원본에 있습니다.
  
    ```R
    rxSummary(formula = ~gender + balance + numTrans + numIntlTrans + creditLine, data = sqlServerDS1)
    ```
  
    실제 결과는 **컴퓨터의 컨텍스트에서** rxSummary [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 를 실행할 때와 같아야 합니다.  그러나 작업은 더 빠르거나 느릴 수 있습니다. 데이터가 분석을 위해 로컬 컴퓨터로 전송되므로 이러한 작업 속도는 데이터베이스에 대한 연결에 크게 좌우됩니다.

## <a name="next-step"></a>다음 단계

[SQL Server 및 XDF 파일 간에 데이터를 이동](../../advanced-analytics/tutorials/deepdive-move-data-between-sql-server-and-xdf-file.md)

## <a name="previous-step"></a>이전 단계

[rxDataStep을 사용하여 청크 분석 수행](../../advanced-analytics/tutorials/deepdive-perform-chunking-analysis-using-rxdatastep.md)
