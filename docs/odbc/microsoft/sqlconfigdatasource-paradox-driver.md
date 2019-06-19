---
title: SQLConfigDataSource (Paradox 드라이버) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLConfigDataSource function [ODBC], Paradox Driver
- Paradox driver [ODBC], SQLConfigDataSource
ms.assetid: 59e84c4e-debe-49d7-b97b-84c736b0c793
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ad9c944af33da86e0d4f85769288f4ab7b6c369f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62665345"
---
# <a name="sqlconfigdatasource-paradox-driver"></a>SQLConfigDataSource(Paradox 드라이버)
> [!NOTE]  
>  이 항목에서는 Paradox 드라이버 관련 정보를 제공 합니다. 이 함수에 대 한 일반 정보에서 해당 항목을 참조 하세요 [ODBC API 참조](../../odbc/reference/syntax/odbc-api-reference.md)합니다.  
  
 합니다 **SQLConfigDataSource** 함수를 추가 하는 데 사용 되는 수정 또는 데이터 원본 삭제 동적으로 다음과 같은 키워드를 사용 합니다.  
  
|키워드|Description|  
|-------------|-----------------|  
|COLLATINGSEQUENCE|필드 정렬 되는 시퀀스입니다.<br /><br /> Paradox 드라이버를 사용 하는 시퀀스 될 수 있습니다 (기본값) ASCII 국제, 스웨덴어-핀란드어, 노르웨이어 덴마크어 합니다.<br /><br /> 동일한 옵션을 설정 **데이터 정렬 시퀀스** 설정 대화 상자에서.|  
|DBQ|데이터베이스 파일의 이름입니다.<br /><br /> 동일한 옵션을 설정 **데이터베이스** 설정 대화 상자에서.|  
|DEFAULTDIR|디렉터리에 경로 지정 합니다.|  
|DESCRIPTION|데이터 원본에 있는 데이터의 설명입니다.<br /><br /> 동일한 옵션을 설정 **설명을** 설정 대화 상자에서.|  
|DRIVER|드라이버 DLL 경로 지정 합니다.|  
|DRIVERID|드라이버에 대 한 정수 ID입니다.<br /><br /> 26 (paradox 3.x)<br /><br /> 282 (paradox 4.x)<br /><br /> 538 (paradox 5.x)|  
|전용|데이터베이스 (한 번에 한 명의 사용자만 액세스할) 단독 모드에서 열립니다 (한 번에 둘 이상의 사용자가 액세스할) 모드를 공유 하는지 여부를 결정 합니다. (단독 모드) true 또는 false (공유 모드) 수 있습니다.<br /><br /> 동일한 옵션을 설정 **배타적** 설정 대화 상자에서.|  
|FIL|파일 형식 Paradox 3.x Paradox 4.x 또는 Paradox 5.x|  
|파일 형식|(텍스트) 텍스트 드라이버에 대 한 파일 형식입니다.|  
|PAGETIMEOUT|1/10 초, 페이지 (사용 되지 않음) 하는 경우 제거 하기 전에 버퍼에 남아 있는 기간을 지정 합니다. 기본값은 600 초 (60 초)의 1/10 초입니다. 이 옵션은 ODBC 드라이버를 사용 하는 모든 데이터 원본에 적용 됩니다 note 합니다.<br /><br /> 동일한 옵션을 설정 **페이지 시간 제한** 설정 대화 상자에서.|  
|PARADOXNETPATH|PDOXUSRS.net 파일을 포함 하기 때문에 Paradox 잠금 데이터베이스를 포함 하는 디렉터리의 전체 경로 (Paradox 4에서. *x*) 또는 PARADOX.net 파일 (Paradox 5에서. *x*). 디렉터리에 이러한 파일 중 하나가 없으면 Paradox 드라이버 하나 만듭니다. 이러한 파일에 대 한 내용은 Paradox 설명서를 참조 하십시오.<br /><br /> 네트워크 디렉터리를 선택할 수 있습니다, 전에 Paradox 사용자 이름을 입력 해야 합니다.<br /><br /> 동일한 옵션을 설정 **네트워크 디렉터리 선택** 설정 대화 상자에서.|  
|PARADOXNETSTYLE|Paradox 드라이버에 대 한 네트워크 액세스 Paradox 데이터에 액세스할 때 사용할 스타일: Paradox 3에 대 한 "3.x" 중 하나입니다. *x* 또는 4에는 "4.x". *x* 5 또는. *x*합니다. Paradox 4 버전이 "3.x" 또는 "4.x"를 설정할 수 있습니다. *x* 5 또는. *x*같으면 버전이 Paradox 3. *x*, 스타일 "3.x" 여야 합니다.<br /><br /> 동일한 옵션을 설정 **Net 스타일** 설정 대화 상자에서.|  
|PARADOXUSERNAME|Paradox 드라이버의 경우 Paradox 사용자 이름입니다.<br /><br /> 동일한 옵션을 설정 **사용자 이름** 설정 대화 상자에서.|  
|PWD|암호입니다.<br /><br /> 이 선택적 키워드 및 드라이버에 의해 파일에 기록 되지 않습니다. 에 대 한 호출에 사용 됩니다 **SQLDriverConnect** Paradox 파일 암호 보호. 테이블을 열 때마다 사용 되는 암호를 잘못 됩니다. 암호가 연결 문자열에 전달 되 면 해당 테이블에 대해 암호가 설정 됩니다. 테이블에 서로 다른 암호를 동일한 세션에서 열 수 없습니다 둘 이상의 않으며 테이블을 조인할 수 없습니다.|  
|READONLY|읽기 전용 파일을 확인. 읽기 전용 파일을 만들기 위해 FALSE입니다.<br /><br /> 동일한 옵션을 설정 **읽기 전용** 설정 대화 상자에서.|  
|스레드|사용 하도록 엔진에 대 한 백그라운드 스레드의 수입니다. 이 값은 3 및 변경할 수 없습니다.<br /><br /> 동일한 옵션을 설정 **스레드** 설정 대화 상자에서.|
