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
ms.openlocfilehash: 33cc778d921b90a460dab6bda352fd7627d2cf7b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68054076"
---
# <a name="sqlconfigdatasource-paradox-driver"></a>SQLConfigDataSource(Paradox 드라이버)
> [!NOTE]  
>  이 항목에서는 Paradox 드라이버 관련 정보를 제공 합니다. 이 함수에 대 한 일반 정보는 [ODBC API 참조](../../odbc/reference/syntax/odbc-api-reference.md)에서 적절 한 항목을 참조 하세요.  
  
 데이터 원본을 추가, 수정 또는 삭제 하는 데 사용 되는 **SQLConfigDataSource** 함수는 다음 키워드를 사용 합니다.  
  
|키워드|Description|  
|-------------|-----------------|  
|COLLATINGSEQUENCE|필드가 정렬 되는 순서입니다.<br /><br /> Paradox 드라이버를 사용 하는 경우 시퀀스는 ASCII (기본값), 국제, 스웨덴어-핀란드어 또는 노르웨이어-덴마크어가 될 수 있습니다.<br /><br /> 이 옵션은 설정 대화 상자에서 **정렬 순서** 와 동일한 옵션을 설정 합니다.|  
|DBQ|데이터베이스 파일의 이름입니다.<br /><br /> 이 옵션은 설치 대화 상자에서 **데이터베이스** 와 동일한 옵션을 설정 합니다.|  
|DEFAULTDIR|디렉터리에 대 한 경로 지정입니다.|  
|설명|데이터 원본의 데이터에 대 한 설명입니다.<br /><br /> 그러면 설정 대화 상자에서 **설명과** 동일한 옵션을 설정 합니다.|  
|DRIVER|드라이버 DLL에 대 한 경로 사양입니다.|  
|DRIVERID|드라이버의 정수 ID입니다.<br /><br /> 26 (Paradox 3(sp3))<br /><br /> 282 (Paradox 4.x)<br /><br /> 538 (Paradox 5.x)|  
|함께|데이터베이스를 단독 모드로 열지 (한 번에 한 명의 사용자만 액세스) 또는 공유 모드 (한 번에 둘 이상의 사용자가 액세스)에서 열지 여부를 결정 합니다. True (배타 모드) 또는 false (공유 모드) 일 수 있습니다.<br /><br /> 그러면 설치 대화 상자에서 **단독** 으로 동일한 옵션을 설정 합니다.|  
|FIL|파일 형식 paradox 3(sp3), paradox 4.x 또는 Paradox .x|  
|FILETYPE|텍스트 드라이버 (텍스트)의 파일 형식입니다.|  
|PAGETIMEOUT|페이지가 제거 되기 전에 버퍼에 유지 되는 시간 (초)을 지정 합니다. 기본값은 600 1/10 초 (60 초)입니다. 이 옵션은 ODBC 드라이버를 사용 하는 모든 데이터 원본에 적용 됩니다.<br /><br /> 설정 대화 상자에서 **페이지 시간 제한과** 같은 옵션을 설정 합니다.|  
|PARADOXNETPATH|PDOXUSRS.net 파일 (Paradox 4)이 포함 되어 있기 때문에 Paradox 잠금 데이터베이스를 포함 하는 디렉터리의 전체 경로입니다.* x*) 또는 PARADOX.net 파일 (PARADOX 5* ) x*). 디렉터리에 이러한 파일 중 하나가 포함 되어 있지 않으면 Paradox 드라이버가 하나를 만듭니다. 이러한 파일에 대 한 자세한 내용은 Paradox 설명서를 참조 하세요.<br /><br /> 네트워크 디렉터리를 선택 하기 전에 Paradox 사용자 이름을 입력 해야 합니다.<br /><br /> 이 옵션은 설치 대화 상자에서 **네트워크 디렉터리 선택** 과 동일한 옵션을 설정 합니다.|  
|PARADOXNETSTYLE|Paradox 드라이버의 경우 paradox 데이터에 액세스할 때 사용할 네트워크 액세스 스타일입니다. Paradox 3의 경우 "3(sp3)"입니다. Paradox 4의 경우 *x* 또는 "4.x"입니다. *x* 또는 5입니다. *x*. 버전은 Paradox 4 인 경우 "3.x" 또는 "4.x"로 설정할 수 있습니다. *x* 또는 5입니다. *x*; 버전이 Paradox 3 인 경우 *x*의 경우 스타일은 "3(sp3)" 이어야 합니다.<br /><br /> 이 옵션은 설치 대화 상자에서 **Net 스타일** 과 동일한 옵션을 설정 합니다.|  
|PARADOXUSERNAME|Paradox 드라이버의 경우 Paradox 사용자 이름입니다.<br /><br /> 이 옵션은 설치 대화 상자에서 **사용자 이름과** 동일한 옵션을 설정 합니다.|  
|PWD|암호입니다.<br /><br /> 이는 선택적 키워드 이며 드라이버에서 파일에 기록 되지 않습니다. 암호 보안 Paradox 파일에 대해 **SQLDriverConnect** 을 호출 하는 데 사용 됩니다. 사용 된 암호는 테이블이 열릴 때마다 유효 합니다. 연결 문자열에 암호가 전달 되지 않으면 해당 테이블에 대 한 암호가 설정 되지 않습니다. 테이블에 다른 암호가 있으면 동일한 세션에서 두 개 이상의를 열 수 없으며 테이블을 조인할 수 없습니다.|  
|READONLY|파일을 읽기 전용으로 설정 하려면 TRUE로 설정 합니다. FALSE 이면 파일을 읽기 전용으로 설정 합니다.<br /><br /> 이 옵션은 설정 대화 상자에서 **읽기 전용** 과 동일한 옵션을 설정 합니다.|  
|임계값|엔진에서 사용할 백그라운드 스레드 수입니다. 이 값은 3 이며 변경할 수 없습니다.<br /><br /> 설정 대화 상자에서 **스레드와** 동일한 옵션을 설정 합니다.|
