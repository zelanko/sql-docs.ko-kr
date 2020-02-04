---
title: '방법: SQLSRV 드라이버를 사용하여 매개 변수 방향 지정 | Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- stored procedure support
ms.assetid: 1209eeca-df75-4283-96dc-714f39956b95
author: MightyPen
ms.author: genemi
ms.openlocfilehash: bf8169b2efa1c3016e98b61b34e9710635ac0d76
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/31/2020
ms.locfileid: "67993372"
---
# <a name="how-to-specify-parameter-direction-using-the-sqlsrv-driver"></a>방법: SQLSRV 드라이버를 사용하여 매개 변수 방향 지정
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

이 항목에서는 SQLSRV 드라이버를 사용하여 저장 프로시저를 호출할 때 매개 변수 방향을 지정하는 방법을 설명합니다. 매개 변수 방향은 [sqlsrv_query](../../connect/php/sqlsrv-query.md) 또는 [sqlsrv_prepare](../../connect/php/sqlsrv-prepare.md)에 전달되는 매개 변수 배열(3단계)을 구성할 때 지정됩니다.  
  
### <a name="to-specify-parameter-direction"></a>매개 변수 방향을 지정하려면  
  
1.  저장 프로시저를 호출하는 Transact-SQL 쿼리를 정의합니다. 저장 프로시저에 전달할 매개 변수 대신 물음표(?)를 사용합니다. 예를 들어 이 문자열은 두 개의 매개 변수를 허용하는 저장 프로시저(UpdateVacationHours)를 호출합니다.  
  
    ```  
    $tsql = "{call UpdateVacationHours(?, ?)}";  
    ```  
  
    > [!NOTE]  
    > 권장되는 방법은 정식 구문을 사용하여 저장 프로시저를 호출하는 것입니다. 정식 구문에 대한 자세한 내용은 [저장 프로시저 호출](../../relational-databases/native-client-odbc-stored-procedures/calling-a-stored-procedure.md)을 참조하세요.  
  
2.  Transact-SQL 쿼리의 자리 표시자에 해당하는 PHP 변수를 초기화하거나 업데이트합니다. 예를 들어 다음 코드는 UpdateVacationHours 저장 프로시저에 대한 두 개의 매개 변수를 초기화합니다.  
  
    ```  
    $employeeId = 101;  
    $usedVacationHours = 8;  
    ```  
  
    > [!NOTE]  
    > 초기화되거나 **null**, **날짜/시간**또는 스트림 형식으로 업데이트되는 변수는 출력 매개 변수로 사용할 수 없습니다.  
  
3.  2단계의 PHP 변수를 사용하여 Transact-SQL  문자열의 매개 변수 자리 표시자에 순서대로 해당 매개 변수 값의 배열을 만들거나 업데이트합니다. 배열에서 각 매개 변수의 방향을 지정합니다. 각 매개 변수의 방향은 두 가지 방법 중 하나로 결정됩니다. 즉, 입력 매개 변수는 기본값, 출력 매개 변수 및 양방향 매개 변수는 **SQLSRV_PARAM_\*** 상수를 사용합니다. 예를 들어 다음 코드는 입력 매개 변수로 *$employeeId* 매개 변수를 지정하고 양방향 매개 변수로 *$usedVacationHours* 매개 변수를 지정합니다.  
  
    ```  
    $params = array(  
                     array($employeeId, SQLSRV_PARAM_IN),  
                     array($usedVacationHours, SQLSRV_PARAM_INOUT)  
                    );  
    ```  
  
    일반적으로 매개 변수 방향을 지정하는 구문을 이해하기 위해 *$var1*, *$var2*및 *$var3* 이 각각 입력, 출력, 양방향 매개 변수에 해당한다고 가정합니다. 다음 방법 중 하나로 매개 변수 방향을 지정할 수 있습니다.  
  
    -   입력 매개 변수를 암시적으로 지정하고 출력 매개 변수 및 양방향 매개 변수를 명시적으로 지정합니다.  
  
        ```  
        array(   
               array($var1),  
               array($var2, SQLSRV_PARAM_OUT),  
               array($var3, SQLSRV_PARAM_INOUT)  
               );  
        ```  
  
    -   입력 매개 변수를 명시적으로 지정하고 출력 매개 변수 및 양방향 매개 변수를 명시적으로 지정합니다.  
  
        ```  
        array(   
               array($var1, SQLSRV_PARAM_IN),  
               array($var2, SQLSRV_PARAM_OUT),  
               array($var3, SQLSRV_PARAM_INOUT)  
               );  
        ```  
  
4.  [sqlsrv_query](../../connect/php/sqlsrv-query.md) 또는 [sqlsrv_prepare](../../connect/php/sqlsrv-prepare.md) 및 [sqlsrv_execute](../../connect/php/sqlsrv-execute.md)를 사용하여 쿼리를 실행합니다. 예를 들어 다음 코드는 *$params* 에서 지정된 매개 변수 값으로 *$tsql* 쿼리를 실행하기 위해 *$conn*연결을 사용합니다.  
  
    ```  
    sqlsrv_query($conn, $tsql, $params);  
    ```  
  
## <a name="see-also"></a>참고 항목  
[방법: SQLSRV 드라이버를 사용하여 출력 매개 변수 검색](../../connect/php/how-to-retrieve-output-parameters-using-the-sqlsrv-driver.md)

[방법: SQLSRV 드라이버를 사용하여 입력 및 출력 매개 변수 검색](../../connect/php/how-to-retrieve-input-and-output-parameters-using-the-sqlsrv-driver.md)  
  
