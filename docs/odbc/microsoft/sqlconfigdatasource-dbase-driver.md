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
ms.openlocfilehash: 569a83110d7d5a3cd25eed8f68753d13793f8b10
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68054103"
---
# <a name="sqlconfigdatasource-dbase-driver"></a>SQLConfigDataSource(dBASE 드라이버)
> [!NOTE]  
>  이 항목에서는 dBASE 드라이버 관련 정보를 제공 합니다. 이 함수에 대 한 일반 정보는 [ODBC API 참조](../../odbc/reference/syntax/odbc-api-reference.md)에서 적절 한 항목을 참조 하세요.  
  
 데이터 원본을 추가, 수정 또는 삭제 하는 데 사용 되는 **SQLConfigDataSource** 함수는 다음 키워드를 사용 합니다.  
  
|키워드|Description|  
|-------------|-----------------|  
|COLLATINGSEQUENCE|필드가 정렬 되는 순서입니다.<br /><br /> 이 시퀀스는 ASCII (기본값) 또는 국제 일 수 있습니다.<br /><br /> 이 옵션은 설정 대화 상자에서 **정렬 순서** 와 동일한 옵션을 설정 합니다.|  
|DEFAULTDIR|디렉터리에 대 한 경로 지정입니다.|  
|DELETED|DBASE 드라이버의 경우 삭제 된 것으로 표시 된 행을 검색 하거나 배치할 수 있는지 여부를 지정 합니다. 1로 설정 된 경우 삭제 된 행은 표시 되지 않습니다. 0으로 설정 하면 삭제 된 행이 삭제 되지 않은 행과 동일 하 게 처리 됩니다.<br /><br /> 이렇게 하면 설치 대화 상자에서 **삭제 된 행 표시** 와 동일한 옵션이 설정 됩니다.|  
|설명|데이터 원본의 데이터에 대 한 설명입니다.<br /><br /> 그러면 설정 대화 상자에서 **설명과** 동일한 옵션을 설정 합니다.|  
|DRIVER|드라이버 DLL에 대 한 경로 사양입니다.|  
|DRIVERID|드라이버의 정수 ID입니다.<br /><br /> 21 (dBASE III)<br /><br /> 277 (dBASE IV)<br /><br /> 533 (dBASE 5.0)|  
|FIL|파일 형식 dBase III, dBase IV 또는 dBase 5|  
|PAGETIMEOUT|페이지가 제거 되기 전에 버퍼에 유지 되는 시간 (초)을 지정 합니다. 기본값은 600 1/10 초 (60 초)입니다. 이 옵션은 ODBC 드라이버를 사용 하는 모든 데이터 원본에 적용 됩니다.<br /><br /> 설정 대화 상자에서 **페이지 시간 제한과** 같은 옵션을 설정 합니다.|  
|READONLY|파일을 읽기 전용으로 설정 하려면 TRUE로 설정 합니다. FALSE 이면 파일을 읽기 전용으로 설정 합니다.<br /><br /> 이 옵션은 설정 대화 상자에서 **읽기 전용** 과 동일한 옵션을 설정 합니다.|  
|STATISTICS|DBASE 드라이버의 경우 테이블 크기 통계의 근사 여부를 결정 합니다. 이 옵션은 ODBC 드라이버를 사용 하는 모든 데이터 원본에 적용 됩니다.<br /><br /> 이 옵션은 설치 대화 상자에서 **대략적인 행 개수** 와 동일한 옵션을 설정 합니다.|  
|임계값|엔진에서 사용할 백그라운드 스레드 수입니다. 이 값은 3 이며 변경할 수 없습니다.<br /><br /> 설정 대화 상자에서 **스레드와** 동일한 옵션을 설정 합니다.|
