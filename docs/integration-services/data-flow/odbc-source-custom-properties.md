---
title: ODBC 원본 사용자 지정 속성 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 362bbcd8-b7b0-4bab-8afe-1212b2ad1af9
caps.latest.revision: 7
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 87ed7a12ae763b0ad40fb0750506ca1ee2be30fe
ms.sourcegitcommit: cc46afa12e890edbc1733febeec87438d6051bf9
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/12/2018
ms.locfileid: "35408355"
---
# <a name="odbc-source-custom-properties"></a>ODBC Source Custom Properties
  다음 표에서는 ODBC 원본의 사용자 지정 속성을 설명합니다. 모든 속성은 SSIS 속성 식에서 설정할 수 있습니다.  
  
|속성 이름|데이터 형식|설명|  
|-------------------|---------------|-----------------|  
|연결|ODBC 연결|원본 데이터베이스에 액세스하기 위한 ODBC 연결입니다.|  
|AccessMode|Integer(열거형)|데이터베이스에 액세스하는 데 사용되는 모드입니다. 가능한 값은 테이블 이름(0) 및 SQL 명령(1)입니다.<br /><br /> 기본값은 테이블 이름(0)입니다.|  
|BatchSize|정수|대량 추출에 대한 일괄 처리 크기입니다. 배열로 추출되는 레코드의 수입니다. 선택한 ODBC 공급자가 배열을 지원하지 않는 경우 일괄 처리 크기는 1입니다.|  
|BindCharColumnAs|Integer(열거형)|이 속성은 ODBC 원본이 다중 바이트 문자열 형식(예: SQL_CHAR, SQL_VARCHAR 또는 SQL_LONGVARCHAR)이 포함된 열을 바인딩하는 방법을 결정합니다.<br /><br /> 가능한 값은 열을 SQL_C_WCHAR로 바인딩하는 유니코드(0)와 열을 SQL_C_CHAR로 바인딩하는 ANSI(1)입니다. 기본값은 유니코드(0)입니다.<br /><br /> **참고**: 이 속성은 **ODBC 원본 편집기**에서 사용할 수 없지만 **고급 편집기**를 사용하여 설정할 수 있습니다.|  
|BindNumericAs|Integer(열거형)|이 속성은 ODBC 원본이 데이터 형식이 SQL_TYPE_NUMERIC 및 SQL_TYPE_DECIMAL인 숫자 데이터가 포함된 열을 바인딩하는 방법을 결정합니다.<br /><br /> 가능한 옵션은 열을 SQL_C_CHAR로 바인딩하는 Char(0)과 열을 SQL_C_NUMERIC으로 바인딩하는 숫자(1)입니다. 기본값은 Char(0)입니다.<br /><br /> **참고**: 이 속성은 **ODBC 원본 편집기**에서 사용할 수 없지만 **고급 편집기**를 사용하여 설정할 수 있습니다.|  
|DefaultCodePage|정수|문자열 출력 열에 사용할 코드 페이지입니다.<br /><br /> **참고**: 이 속성은 **ODBC 원본 편집기**에서 사용할 수 없지만 **고급 편집기**를 사용하여 설정할 수 있습니다.|  
|ExposeCharColumnsAsUnicode|Boolean|이 속성은 구성 요소가 CHAR 열을 표시하는 방법을 결정합니다. 기본값은 CHAR 열이 멀티바이트 문자열(DT_STR)로 표시됨을 나타내는 False입니다. True이면 CHAR 열이 와이드 문자열(DT_WSTR)로 표시됩니다.<br /><br /> **참고**: 이 속성은 **ODBC 원본 편집기**에서 사용할 수 없지만 **고급 편집기**를 사용하여 설정할 수 있습니다.|  
|FetchMethod|Integer(열거형)|데이터를 가져오는 데 사용되는 메서드입니다. 가능한 옵션은 행 단위(0) 및 일괄 처리(1)입니다. 기본값은 일괄 처리(1)입니다.<br /><br /> 이러한 옵션에 대한 자세한 내용은 [ODBC Source](../../integration-services/data-flow/odbc-source.md)를 참조하세요.<br /><br /> **참고**: 이 속성은 **ODBC 원본 편집기**에서 사용할 수 없지만 **고급 편집기**를 사용하여 설정할 수 있습니다.|  
|SqlCommand|String|AccessMode가 SQL 명령으로 설정될 때 실행할 SQL 명령입니다.|  
|StatementTimeout|정수|오류가 발생하여 응용 프로그램으로 반환되기 전에 SQL 문이 실행되기를 기다릴 시간(초)입니다. 기본값은 120입니다. 값 0은 시스템에 제한 시간이 없음을 나타냅니다.|  
|TableName|String|AccessMode가 테이블 이름으로 설정될 때 사용되는 데이터가 포함된 테이블의 이름입니다.|  
|LobChunckSize|정수|LOB 열에 대한 청크 크기 할당입니다.|  
||||  
  
## <a name="see-also"></a>참고 항목  
 [ODBC Source](../../integration-services/data-flow/odbc-source.md)   
 [ODBC 원본 편집기&#40;연결 관리자 페이지&#41;](../../integration-services/data-flow/odbc-source-editor-connection-manager-page.md)  
  
  
