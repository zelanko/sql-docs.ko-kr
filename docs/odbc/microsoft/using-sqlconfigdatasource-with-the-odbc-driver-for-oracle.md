---
title: 오라클의 ODBC 드라이버와 함께 SQLConfigDatasource 사용 | 마이크로 소프트 문서
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 718e444d63e0d4cf3821c0c03eb851732ed5b4e4
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81292773"
---
# <a name="using-sqlconfigdatasource-with-the-odbc-driver-for-oracle"></a>Oracle용 ODBC 드라이버와 SQLConfigDatasource 사용
> [!IMPORTANT]  
>  이 기능은 이후 버전의 Windows에서 제거됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요. 대신 오라클에서 제공하는 ODBC 드라이버를 사용합니다.  
  
 다음 표에는 오라클용 Microsoft ODBC 드라이버, 버전 1.0(Msorcl10.dll) 및 오라클용 Microsoft ODBC 드라이버, 버전 2.0(Msorcl32.dll)에 대한 유효한 **SQLConfigDatasource** 설정이 나열되어 있습니다.  
  
> [!NOTE]  
>  Msorcl10.dll 드라이버(버전 1.0)는 **서버를**제외한 모든 설정을 지원합니다. Msorcl32.dll 드라이버(버전 2.0 이상)는 모든 설정을 지원합니다.  
  
 일부 설정은 드라이버에서 무시되지만 **SQLConfigDatasource에서**허용됩니다. ODBC 연결 문자열에 이러한 설정을 포함하는 것이 런타임에 허용되는 유일한 방법입니다. **SQLConfigDatasource가** 데이터 원본을 만들 때 무시된 설정은 레지스트리에 저장되지 않습니다.  
  
 다음 표에서 *A/N은* 허용되는 최대 길이까지 유효한 영숫자 문자열을 의미합니다. *최대 렌(최대* 길이)은 문자열 종사 문자를 포함하여 설정에서 허용하는 최대 허용 문자열 길이입니다.  
  
|설정|맥스 렌|기본값|유효한 값|설명|  
|-------------|-------------|-------------------|------------------|-----------------|  
|BufferSize|7|65535|1000|최대 65535바이트의 최소 페치 버퍼 크기|  
|카탈로그 캡|2|1|0 또는 1|1이면 표인용되지 않은 식별자가 카탈로그 함수의 대문자로 변환됩니다.|  
|ConnectString|128|""|A/N|연결 문자열. Msorcl10.dll 드라이버를 사용하여 서버 이름을 지정하는 필수 방법입니다.|  
|설명|256|""|A/N|설명|  
|DSN|33|""|A/N|데이터 원본 이름입니다.|  
|추측더콜데프|4|0|A/N|Oracle 정의 배율이 없는 열에 대해 0이 아닌 값을 반환합니다.|  
|숫자 플로트|2|""|0 또는 1|0이면 FLOAT 열이 SQL_FLOAT 처리됩니다. 1이면 FLOAT 열은 SQL_DOUBLE 처리됩니다.|  
|PWD|30|""|A/N|Password.|  
|RDO 지원|2|""|0 또는 1|RDO가 Oracle 프로시저를 호출할 수 있습니다.|  
|설명|2|0|0 또는 1|카탈로그 함수에 비고를 포함합니다.|  
|행 제한|4|""|0 - 99|SELECT 문에서 반환되는 최대 행 수입니다. 길이가 0인 문자열은 제한이 적용되지 않는다는 것을 나타냅니다.|  
|서버|128|""|A/N|오라클 서버 이름.|  
|동의어열|2|1|0 또는 1|SQLColumns에 동의를 포함합니다.|  
|시스템 테이블|2|""|0 또는 1|0이면 시스템 테이블이 표시되지 않습니다. 1이면 시스템 테이블이 표시됩니다.|  
|번역DLL|33|""|A/N|번역 .dll 이름입니다.|  
|번역 이름|33|""|A/N|번역 이름입니다.|  
|번역 옵션|33|""|A/N|번역 옵션.|  
|TxnCap|2|""|A/N|트랜잭션 가능. 0이면 드라이버는 트랜잭션을 지원하지 않는다고 보고합니다. 1이면 드라이버는 트랜잭션을 수행할 수 있다고 보고합니다.|  
|UID|30|""|A/N|사용자 이름.|
