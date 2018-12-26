---
title: Oracle 용 ODBC 드라이버와 SQLConfigDatasource 사용 | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 9edd9ae15e66a39abd84a8a6d8e50a83ed4a39ba
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47779011"
---
# <a name="using-sqlconfigdatasource-with-the-odbc-driver-for-oracle"></a>Oracle용 ODBC 드라이버와 SQLConfigDatasource 사용
> [!IMPORTANT]  
>  이 기능은 Windows의 이후 버전에서 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요. 대신, Oracle에서 제공 하는 ODBC 드라이버를 사용 합니다.  
  
 다음 표에서 유효한 **SQLConfigDatasource** Microsoft ODBC Driver for Oracle 버전 1.0 (Msorcl10.dll) 및 Microsoft ODBC Driver for Oracle (Msorcl32.dll) 2.0 버전에 대 한 설정입니다.  
  
> [!NOTE]  
>  Msorcl10.dll 드라이버 (버전 1.0)을 제외한 모든 설정 지원 **Server**합니다. Msorcl32.dll 드라이버 (버전 2.0 이상)에 모든 설정을 지원합니다.  
  
 일부 설정은 드라이버에 의해 무시 됩니다 있지만 허용할 **SQLConfigDatasource**합니다. ODBC 연결 문자열에서 이러한 설정을 포함 하는 유일한 방법은 런타임 시 허용 됩니다. 무시 되는 설정은 레지스트리에 저장 되지 것입니다 때 **SQLConfigDatasource** 데이터 원본을 만듭니다.  
  
 다음 표에 *A/N* 허용 되는 최대 길이 까지만 유효한 영숫자 문자열을 의미 합니다. *최대 Len* (최대 길이)는 허용 되는 최대 문자열 길이 문자열 종결자 문자를 포함 하 여 설정에서 허용 합니다.  
  
|설정|최대 Len|기본값|유효한 값|Description|  
|-------------|-------------|-------------------|------------------|-----------------|  
|BufferSize|7|65535|1000|최소 인출 버퍼에는 최대 65,535 바이트 크기|  
|CatalogCap|2|1|0 또는 1|1 인 경우 nonquoted 식별자 카탈로그에서 대문자로 변환 된 함수가 됩니다.|  
|ConnectString|128|""|A/N|연결 문자열. 필요한 메서드의 Msorcl10.dll 드라이버를 사용 하 여 서버 이름을 지정 합니다.|  
|Description|256|""|A/N|설명|  
|DSN|33|""|A/N|데이터 원본 이름입니다.|  
|GuessTheColDef|4|0|A/N|Oracle 정의한 확장 없이 열에 대해 0이 아닌 값을 반환합니다.|  
|NumberFloat|2|""|0 또는 1|0 인 경우에 FLOAT 열 SQL_FLOAT로 처리 됩니다. 1 인 경우에 FLOAT 열 SQL_DOUBLE로 처리 됩니다.|  
|PWD|30|""|A/N|암호입니다.|  
|RDOSupport|2|""|0 또는 1|RDO를 Oracle 프로시저를 호출할 수 있습니다.|  
|Remarks|2|0|0 또는 1|카탈로그 함수에 주의 포함 합니다.|  
|RowLimit|4|""|0에서 99 사이의|SELECT 문에서 반환한 행의 최대 수입니다. 길이가 0 인 문자열로 제한이 적용 되지 않음을 나타냅니다.|  
|서버|128|""|A/N|Oracle 서버 이름입니다.|  
|SynonymColumns|2|1|0 또는 1|SQLColumns에 동의어를 포함 합니다.|  
|SystemTable|2|""|0 또는 1|0 인 경우에 시스템 테이블 표시 되지 않습니다. 1 인 경우 시스템 테이블이 표시 됩니다.|  
|TranslationDLL|33|""|A/N|번역.dll 이름입니다.|  
|TranslationName|33|""|A/N|번역 이름입니다.|  
|TranslationOption|33|""|A/N|번역 옵션입니다.|  
|TxnCap|2|""|A/N|트랜잭션을 지원 합니다. 0 인 경우 드라이버는 트랜잭션을 지원 하지 않습니다 보고 합니다. 1 인 경우 드라이버는 트랜잭션을 수행할 수 있는 것을 보고 합니다.|  
|UID|30|""|A/N|사용자 이름입니다.|
