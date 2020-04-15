---
title: SQLConfigDataSource (dBASE 드라이버) | 마이크로 소프트 문서
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 18c6721b4f34772e8c3cd8e4f515233f80566fb3
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81283973"
---
# <a name="sqlconfigdatasource-dbase-driver"></a>SQLConfigDataSource(dBASE 드라이버)
> [!NOTE]  
>  이 항목에서는 dBASE 드라이버 관련 정보를 제공합니다. 이 함수에 대한 일반적인 정보는 [ODBC API 참조](../../odbc/reference/syntax/odbc-api-reference.md)에서 적절한 항목을 참조하십시오.  
  
 데이터 원본을 동적으로 추가, 수정 또는 삭제하는 데 사용되는 **SQLConfigDataSource** 함수는 다음 키워드를 사용합니다.  
  
|키워드|설명|  
|-------------|-----------------|  
|콜라팅시퀀스|필드가 정렬되는 시퀀스입니다.<br /><br /> 시퀀스는 ASCII(기본값) 또는 국제순서일 수 있습니다.<br /><br /> 이렇게 하면 설정 대화 상자에서 **시퀀스 정렬과** 동일한 옵션이 설정됩니다.|  
|기본디더|디렉터리로의 경로 사양입니다.|  
|DELETED|dBASE 드라이버의 경우 삭제된 것으로 표시된 행을 검색하거나 배치할 수 있는지 여부를 지정합니다. 1로 설정하면 삭제된 행이 표시되지 않습니다. 0으로 설정하면 삭제된 행이 삭제되지 않은 행과 동일하게 처리됩니다.<br /><br /> 이렇게 하면 설치 대화 상자에서 **삭제된 행 표시와** 동일한 옵션이 설정됩니다.|  
|설명|데이터 원본의 데이터에 대한 설명입니다.<br /><br /> 이렇게 하면 설정 대화 상자의 **설명과** 동일한 옵션이 설정됩니다.|  
|DRIVER|드라이버 DLL에 대한 경로 사양입니다.|  
|드라이버 ID|드라이버에 대한 정수 ID입니다.<br /><br /> 21 (dBASE III)<br /><br /> 277 (dBASE IV)<br /><br /> 533 (dBASE 5.0)|  
|Fil|파일 형식 dBase III, dBase IV 또는 dBase 5|  
|페이지 시간 시간|페이지(사용하지 않은 경우)가 제거되기 전에 버퍼에 남아 있는 기간을 1초의 10분의 1로 지정합니다. 기본값은 초당 600분의 1초(60초)입니다. 이 옵션은 ODBC 드라이버를 사용하는 모든 데이터 원본에 적용됩니다.<br /><br /> 이렇게 하면 설정 대화 상자에서 **페이지 시간 설정과** 동일한 옵션이 설정됩니다.|  
|READONLY|TRUE는 파일을 읽기 전용으로 만듭니다. FALSE파일을 읽기 전용으로 만들지 않도록 합니다.<br /><br /> 이렇게 하면 설정 대화 상자에서 **만 읽기와** 동일한 옵션이 설정됩니다.|  
|STATISTICS|dBASE 드라이버의 경우 테이블 크기 통계가 근사화되는지 여부를 결정합니다. 이 옵션은 ODBC 드라이버를 사용하는 모든 데이터 원본에 적용됩니다.<br /><br /> 이렇게 하면 설정 대화 상자에서 **대략적인 행 수와** 동일한 옵션이 설정됩니다.|  
|스레드|사용할 엔진의 배경 스레드 수입니다. 이 값은 3이며 변경할 수 없습니다.<br /><br /> 이렇게 하면 설정 대화 상자의 스레드와 동일한 옵션이 **설정됩니다.**|
