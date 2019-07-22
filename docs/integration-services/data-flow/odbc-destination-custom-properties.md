---
title: ODBC 대상 사용자 지정 속성 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 07508c40-6c08-4359-96cd-8ff17671244d
author: janinezhang
ms.author: janinez
ms.openlocfilehash: a5413191366792a64bb3988eb9feb25991bd11c3
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68031291"
---
# <a name="odbc-destination-custom-properties"></a>ODBC Destination Custom Properties

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  다음 표에서는 ODBC 대상의 사용자 지정 속성을 설명합니다. 모든 속성은 SSIS 속성 식에서 설정할 수 있습니다.  
  
|속성 이름|데이터 형식|설명|  
|-------------------|---------------|-----------------|  
|연결|ODBC 연결|대상 데이터베이스에 액세스하기 위한 ODBC 연결입니다.|  
|BatchSize|정수|대량 로드에 대한 일괄 처리 크기입니다. 일괄 처리로 로드되는 행의 개수입니다. 행 단위 매개 변수 바인딩이 지원되는 경우에만 유효합니다. 행 단위 매개 변수 바인딩이 지원되지 않는 경우에는 일괄 처리 크기가 1입니다.|  
|BindCharColumnAs|Integer(열거형)|이 속성은 ODBC 대상이 다중 바이트 문자열 형식(예: SQL_CHAR, SQL_VARCHAR 또는 SQL_LONGVARCHAR)이 포함된 열을 바인딩하는 방법을 결정합니다.<br /><br /> 가능한 값은 열을 SQL_C_WCHAR로 바인딩하는 유니코드(0)와 열을 SQL_C_CHAR로 바인딩하는 ANSI(1)입니다. 기본값은 유니코드(0)입니다.<br /><br /> 유니코드는 대부분의 ODBC 3.x 공급자와 CHAR 매개 변수를 와이드 문자열로 바인딩하는 작업을 지원하는 ODBC 2.x 공급자가 사용할 수 있는 최상의 옵션입니다. 유니코드를 선택하고 ExposeCharColumnsAsUnicode가 True인 경우 사용자가 원본 데이터베이스에 사용되는 코드 페이지를 지정하지 않아도 됩니다.<br /><br /> **참고:** 이 속성은 **ODBC 대상 편집기**에서 사용할 수 없지만 **고급 편집기**를 사용하여 설정할 수 있습니다.|  
|BindNumericAs|Integer(열거형)|이 속성은 ODBC 대상이 데이터 형식이 SQL_TYPE_NUMERIC 및 SQL_TYPE_DECIMAL인 숫자 데이터가 포함된 열을 바인딩하는 방법을 결정합니다.<br /><br /> 가능한 값은 열을 SQL_C_CHAR로 바인딩하는 Char(0)과 열을 SQL_C_NUMERIC으로 바인딩하는 숫자(1)입니다. 기본값은 Char(0)입니다.<br /><br /> **참고**: 이 속성은 **ODBC 대상 편집기**에서 사용할 수 없지만 **고급 편집기**를 사용하여 설정할 수 있습니다.|  
|DefaultCodePage|정수|문자열 열에 사용할 코드 페이지입니다.<br /><br /> **참고**: 이 속성은 **ODBC 대상 편집기**에서 사용할 수 없지만 **고급 편집기**를 사용하여 설정할 수 있습니다.|  
|InsertMethod|Integer(열거형)|데이터 삽입에 사용되는 메서드입니다. 가능한 값은 행 단위(0) 및 일괄 처리(1)입니다. 기본값은 일괄 처리(1)입니다.<br /><br /> 이러한 옵션에 대한 자세한 내용은 [ODBC Destination](../../integration-services/data-flow/odbc-destination.md)의 "로드 옵션"을 참조하세요.|  
|StatementTimeout|정수|오류가 발생하여 애플리케이션으로 반환되기 전에 SQL 문이 실행되기를 기다릴 시간(초)입니다. 기본값은 120입니다.|  
|TableName|String|데이터가 삽입되는 대상 테이블의 이름입니다.|  
|TransactionSize|정수|단일 트랜잭션의 삽입 수입니다. 기본값은 ODBC 대상이 자동 커밋 모드에서 작동함을 의미하는 0입니다.<br /><br /> ODBC 연결 관리자는 분산 트랜잭션을 지원하지 않으므로 이 속성을 0 이외의 값으로 설정할 수 있습니다. 그러나 연결 관리자 **RetainSameConnection** 속성이 **true** 로 설정된 경우에는 이 속성을 0으로 설정해야 합니다.<br /><br /> **참고**: 이 속성은 **ODBC 대상 편집기**에서 사용할 수 없지만 **고급 편집기**를 사용하여 설정할 수 있습니다.|  
|LobChunkSize|정수|LOB 열에 대한 청크 크기 할당입니다.|  
  
  
