---
title: SQLConfigDataSource (dBASE 드라이버) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- DBase driver [ODBC], SQLConfigDataSource
- SQLConfigDataSource function [ODBC], dBASE Driver
ms.assetid: 19909902-054c-4e19-9c06-a212aace13fe
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 63d1951cfe835cbfca23ab366db2216215aa92c3
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47631651"
---
# <a name="sqlconfigdatasource-dbase-driver"></a>SQLConfigDataSource(dBASE 드라이버)
> [!NOTE]  
>  이 항목에서는 dBASE 드라이버 관련 정보를 제공 합니다. 이 함수에 대 한 일반 정보에서 해당 항목을 참조 하세요 [ODBC API 참조](../../odbc/reference/syntax/odbc-api-reference.md)합니다.  
  
 합니다 **SQLConfigDataSource** 함수를 추가 하는 데 사용 되는 수정 또는 데이터 원본 삭제 동적으로 다음과 같은 키워드를 사용 합니다.  
  
|키워드|Description|  
|-------------|-----------------|  
|COLLATINGSEQUENCE|필드 정렬 되는 시퀀스입니다.<br /><br /> 시퀀스 될 수 있습니다: ASCII (기본값) 또는 International입니다.<br /><br /> 동일한 옵션을 설정 **데이터 정렬 시퀀스** 설정 대화 상자에서.|  
|DEFAULTDIR|디렉터리에 경로 지정 합니다.|  
|DELETED|DBASE 드라이버의 경우 삭제 된 것으로 표시 된 행을 검색 하거나 배치할 수 있는지 여부를 지정 합니다. 삭제 된 행을 1로 표시 되지 않으면; 삭제 된 행을 0으로 설정 되 면 삭제 되지 않은 행으로 동일 하 게 처리 합니다.<br /><br /> 동일한 옵션을 설정 **삭제 된 행 표시** 설정 대화 상자에서.|  
|DESCRIPTION|데이터 원본에 있는 데이터의 설명입니다.<br /><br /> 동일한 옵션을 설정 **설명을** 설정 대화 상자에서.|  
|DRIVER|드라이버 DLL 경로 지정 합니다.|  
|DRIVERID|드라이버에 대 한 정수 ID입니다.<br /><br /> 21 (dBASE III)<br /><br /> 277 (dBASE IV)<br /><br /> 533 (dBASE 5.0)|  
|FIL|파일 dBase III, IV, dBase 또는 dBase 5 입력 합니다.|  
|PAGETIMEOUT|1/10 초, 페이지 (사용 되지 않음) 하는 경우 제거 하기 전에 버퍼에 남아 있는 기간을 지정 합니다. 기본값은 600 초 (60 초)의 1/10 초입니다. 이 옵션은 ODBC 드라이버를 사용 하는 모든 데이터 원본에 적용 됩니다 note 합니다.<br /><br /> 동일한 옵션을 설정 **페이지 시간 제한** 설정 대화 상자에서.|  
|READONLY|읽기 전용 파일을 확인. 읽기 전용 파일을 만들기 위해 FALSE입니다.<br /><br /> 동일한 옵션을 설정 **읽기 전용** 설정 대화 상자에서.|  
|STATISTICS|DBASE 드라이버의 경우 테이블 크기 통계는 계산 하는지 여부를 결정 합니다. 이 옵션은 ODBC 드라이버를 사용 하는 모든 데이터 원본에 적용 됩니다 note 합니다.<br /><br /> 동일한 옵션을 설정 **대략적인 행 개수** 설정 대화 상자에서.|  
|스레드|사용 하도록 엔진에 대 한 백그라운드 스레드의 수입니다. 이 값이 3이 고 변경할 수 없습니다.<br /><br /> 동일한 옵션을 설정 **스레드** 설정 대화 상자에서.|
