---
title: Oracle 용 ODBC 드라이버와 함께 SQLConfigDatasource 사용 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLConfigDataSource function [ODBC], ODBC driver for Oracle
ms.assetid: e535d1ef-aff9-4ae7-a3ed-ef4ca2584289
author: MightyPen
ms.author: genemi
ms.openlocfilehash: fa5f1ecf9f3100480081e3744fc7d280a4da282b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68088028"
---
# <a name="using-sqlconfigdatasource-with-the-odbc-driver-for-oracle"></a>Oracle용 ODBC 드라이버와 SQLConfigDatasource 사용
> [!IMPORTANT]  
>  이 기능은 이후 버전의 Windows에서 제거 될 예정입니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요. 대신 Oracle에서 제공 하는 ODBC 드라이버를 사용 합니다.  
  
 다음 표에서는 Oracle 용 Microsoft ODBC 드라이버 버전 1.0 (Msorcl10) 및 Microsoft ODBC Driver for Oracle, 버전 2.0 (Msorcl32)에 대 한 유효한 **SQLConfigDatasource** 설정을 보여 줍니다.  
  
> [!NOTE]  
>  Msorcl10 드라이버 (버전 1.0)는 **서버**를 제외한 모든 설정을 지원 합니다. Msorcl32 드라이버 (버전 2.0 이상)는 모든 설정을 지원 합니다.  
  
 일부 설정은 드라이버에서 무시 되지만 **SQLConfigDatasource**에서 허용 됩니다. 이러한 설정을 ODBC 연결 문자열에 포함 하는 것은 런타임에 허용 되는 유일한 방법입니다. **SQLConfigDatasource** 에서 데이터 원본을 만들 때 무시 된 설정이 레지스트리에 저장 되지 않습니다.  
  
 다음 표에서 *A/N은* 최대 허용 길이 까지의 유효한 영숫자 문자열을 의미 합니다. *Max Len* (최대 길이)은 문자열-종결자 문자를 포함 하 여 설정에서 허용 하는 최대 허용 문자열 길이입니다.  
  
|설정|최대 Len|기본값|유효한 값|Description|  
|-------------|-------------|-------------------|------------------|-----------------|  
|BufferSize|7|65535|1000|최대 65535 바이트의 최소 인출 버퍼 크기|  
|CatalogCap|2|1|0 또는 1|1 인 경우 따옴표 붙지 않은 식별자는 카탈로그 함수에서 대문자로 변환 됩니다.|  
|ConnectString|128|""|A/N|연결 문자열. Msorcl10 드라이버를 사용 하 여 서버 이름을 지정 하는 데 필요한 메서드입니다.|  
|Description|256|""|A/N|설명|  
|DSN|33|""|A/N|데이터 원본 이름입니다.|  
|GuessTheColDef|4|0|A/N|Oracle에서 정의한 소수 자릿수가 없는 열에 대해 0이 아닌 값을 반환 합니다.|  
|숫자 Float|2|""|0 또는 1|0 인 경우 FLOAT 열은 SQL_FLOAT로 처리 됩니다. 1 인 경우 FLOAT 열은 SQL_DOUBLE로 처리 됩니다.|  
|PWD|30|""|A/N|Password.|  
|RDOSupport|2|""|0 또는 1|RDO에서 Oracle 프로시저를 호출할 수 있도록 합니다.|  
|설명|2|0|0 또는 1|카탈로그 함수에 설명을 포함 합니다.|  
|RowLimit|4|""|0 ~ 99|SELECT 문에 의해 반환 되는 최대 행 수입니다. 길이가 0 인 문자열은 제한이 적용 되지 않음을 나타냅니다.|  
|서버|128|""|A/N|Oracle 서버 이름입니다.|  
|SynonymColumns|2|1|0 또는 1|SQLColumns에 동의어를 포함 합니다.|  
|SystemTable|2|""|0 또는 1|0 인 경우 시스템 테이블은 표시 되지 않습니다. 1 인 경우 시스템 테이블이 표시 됩니다.|  
|TranslationDLL|33|""|A/N|변환 .dll 이름입니다.|  
|TranslationName|33|""|A/N|번역 이름.|  
|TranslationOption|33|""|A/N|Translation 옵션입니다.|  
|TxnCap|2|""|A/N|트랜잭션을 사용할 수 있습니다. 0 인 경우 드라이버가 트랜잭션을 지원 하지 않는다는 것을 보고 합니다. 1 인 경우 드라이버는 트랜잭션을 수행할 수 있음을 보고 합니다.|  
|UID|30|""|A/N|사용자 이름.|
