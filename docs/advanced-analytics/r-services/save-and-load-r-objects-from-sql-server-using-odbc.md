---
title: "ODBC를 사용하여 SQL Server에서 R 개체 저장 및 로드 | Microsoft Docs"
ms.custom: ""
ms.date: "12/16/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "R"
ms.assetid: 6ac2e971-6b4f-4c73-ba57-29c716abd057
caps.latest.revision: 8
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 8
---
# ODBC를 사용하여 SQL Server에서 R 개체 저장 및 로드
SQL Server R Services는 직렬화된 R 개체를 테이블에 저장한 다음 R 코드를 다시 실행하거나 모델을 다시 학습시키지 않고 필요에 따라 테이블에서 개체를 로드할 수 있습니다. R 개체를 데이터베이스에 저장하는 이 기능은 모델을 교육하고 저장한 다음 점수 매기기나 분석을 위해 나중에 사용하는 시나리오에서 매우 중요합니다. 

이 중요한 단계의 성능을 개선하기 위해 이제 **RevoScaleR** 패키지에는 성능을 현저하게 향상시키고 개체를 보다 조밀하게 저장하는 직렬화 및 역직렬화 함수가 포함됩니다. 또한 *RxOdbcData*를 사용하는 ODBC 연결을 통해 이러한 새 함수를 호출하여 R 환경에서 직접 SQL Server에 R 개체를 저장할 수 있습니다.

## <a name="overview"></a>개요

이제 **RevoScaleR** 패키지에는 보다 쉽게 SQL Server에 R 개체를 저장한 다음 SQL Server 테이블에서 개체를 읽을 수 있도록 하는 새 함수가 포함됩니다. 이러한 함수를 사용하려면 *RxOdbcData* 데이터 원본을 사용하여 SQL Server에 대한 연결을 설정해야 합니다.

일반적으로 함수 호출은 키가 개체의 이름인 간단한 키 값 저장소에 따라 모델링되며 키와 연결된 값은 테이블 내부 또는 외부로 이동할 varbinary R 개체입니다. 

- 기본적으로 SQL Server로 이동하기 위해 R에서 호출하는 모든 개체는 직렬화되고 압축됩니다. 
- 반대로 R 코드에서 사용하기 위해 SQL Server 테이블에서 개체를 로드하는 경우 개체는 역직렬화되고 압축이 풀립니다.
- 필요에 따라 개체를 직렬화하지 않도록 지정할 수 있으며 기본 압축 알고리즘 대신 사용할 새 압축 알고리즘을 선택할 수 있습니다.


## <a name="new-functions"></a>새로운 함수

- `rxWriteObject`는 ODBC 데이터 원본을 사용하여 SQL Server에 R 개체를 씁니다. 

- `rxReadObject`는 ODBC 데이터 원본을 사용하여 SQL Server 데이터베이스에서 R 개체를 읽습니다.

- `rxDeleteObject`는 ODBC 데이터 원본에 지정된 SQL Server 데이터베이스에서 R 개체를 삭제합니다. 키/버전 조합으로 식별되는 개체가 여러 개 있을 경우 모두 삭제됩니다.

- `rxListKeys`는 사용 가능한 모든 개체를 키-값 쌍으로 나열합니다. 따라서 R 개체의 이름 및 버전을 확인하는 데 도움이 됩니다.

각 함수의 구문에 대한 자세한 도움말을 보려면 R 도움말을 사용하세요. 자세한 내용은 나중에 MSDN의 [ScaleR reference](https://msdn.microsoft.com/microsoft-r/scaler/scaler)(ScaleR 참조)에서 확인할 수 있습니다.

## <a name="how-to-store-r-objects-in-sql-server-using-odbc"></a>ODBC를 사용하여 SQL Server에 R 개체를 저장하는 방법

이 절차에서는 새 함수를 사용하여 모델을 만들고 SQL Server에 저장하는 방법을 보여 줍니다.

1. SQL Server에 대한 연결 문자열을 설정합니다.
   ```R
   conStr <- 'Driver={SQL Server};Server=localhost;Database=storedb;Trusted_Connection=true'
   ```
2. 연결 문자열을 사용하여 R에 *rxOdbcData* 데이터 원본 개체를 만듭니다.
   ```R
   ds <- RxOdbcData(table="robjects", connectionString=conStr)
   ```

3. 테이블이 이미 있는 경우 삭제하고 이전 버전의 개체를 추적하지 않으려고 합니다.

   ```R
   if(rxSqlServerTableExists(ds@table, ds@connectionString)) {
       rxSqlServerDropTable(ds@table, ds@connectionString)
       }
   ```
   
4. 이진 개체를 저장하는 데 사용할 수 있는 테이블을 정의합니다.

   ```R
   ddl <- paste(" CREATE TABLE [", ds@table, "] 
      (","  [id] varchar(200) NOT NULL,
       "," [value] varbinary(max),
       "," CONSTRAINT unique_id UNIQUE (id))", 
       sep = "") 
   ```
5. ODBC 연결을 열어 테이블을 만들고 DDL 문이 완료되면 연결을 닫습니다.

   ```R
    rxOpen(ds, "w") 
    rxExecuteSQLDDL(ds, ddl) 
    rxClose(ds)
    ```
6. 저장하려는 R 개체를 생성합니다.

   ```R
   infertLogit <- rxLogit(case ~ age + parity + education + spontaneous + induced, 
     data = infert)
   ```
6. 앞에서 만든 *RxOdbcData* 개체를 사용하여 모델을 데이터베이스에 저장합니다.

   ```R
   rxWriteObject(ds, "logit.model", infertLogit)
   ```

## <a name="how-to-read-r-objects-from-sql-server-using-odbc"></a>ODBC를 사용하여 SQL Server에서 R 개체를 읽는 방법

이 절차에서는 새 함수를 사용하여 SQL Server에서 모델을 로드하는 방법을 보여 줍니다.

1. SQL Server에 대한 연결 문자열을 설정합니다.

   ```R
   conStr2 <- 'Driver={SQL Server};Server=localhost;Database=storedb;Trusted_Connection=true'
   ```
2. 연결 문자열을 사용하여 R에 *rxOdbcData* 데이터 원본 개체를 만듭니다.

   ```R
   ds <- RxOdbcData(table="robjects", connectionString=conStr2)
   ```
3. 해당 R 개체 이름을 지정하여 테이블에서 모델을 읽습니다.

   ```R
    infertLogit2 <- rxReadObject(ds, "logit.model")
   ```

## <a name="see-also"></a>참고 항목

[R Services 기능 및 작업](../../advanced-analytics/r-services/sql-server-r-services-features-and-tasks.md)
