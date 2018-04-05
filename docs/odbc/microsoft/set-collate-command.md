---
title: SET COLLATE 명령을 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- set collate command [ODBC]
ms.assetid: 00efbcd4-fea8-4061-86a5-82de413cb753
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 735e28da49e0c8a9dc3a12d9a29d107209ec99dd
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/21/2017
---
# <a name="set-collate-command"></a>SET COLLATE 명령
후속 인덱싱 및 정렬 작업의 문자 필드에 대 한 데이터 정렬 순서를 지정합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
SET COLLATE TO cSequenceName  
```  
  
## <a name="arguments"></a>인수  
 *cSequenceName*  
 데이터 정렬 순서를 지정합니다. 사용 가능한 데이터 정렬 순서 옵션을 다음 표에 설명 되어 있습니다.  
  
|변수|언어|  
|-------------|--------------|  
|네덜란드어|네덜란드어|  
|GENERAL|영어, 프랑스어, 독일어, 최신 스페인어, 포르투갈어, 및 기타 서유럽 언어|  
|독일어|독일어 전화 번호부 순서 (DIN)|  
|아이슬란드|아이슬란드어|  
|컴퓨터|컴퓨터 (이전 FoxPro 버전에 대 한 기본 데이터 정렬 순서)|  
|NORDAN|노르웨이어, 덴마크어|  
|스페인어|스페인어|  
|SWEFIN|스웨덴어, 핀란드어|  
|UNIQWT|고유 가중치|  
  
> [!NOTE]  
>  스페인어 옵션을 지정 하면 *ch* 사이 정렬 하는 단일 문자는 *c* 및 *d*, 및 *ll* 간의 정렬  *l* 및 *m*합니다.  
  
 리터럴 문자열 데이터 정렬 순서 옵션을 지정 하는 경우 따옴표 안에 옵션을 포함 해야 합니다.  
  
```  
SET COLLATE TO "SWEFIN"  
```  
  
 컴퓨터의 기본 데이터 정렬 순서 옵션이 이며 시퀀스 Xbase 사용자를 잘 알고 있습니다. 문자가 현재 코드 페이지에 나타나는 순서 대로 정렬 됩니다.  
  
 일반 미국과 서유럽어 사용자가 더 적합할 수 있습니다. 문자가 현재 코드 페이지에 나타나는 순서 대로 정렬 됩니다. FoxPro 버전에서 2.5에서는 이전 인덱스 작성 되었을 사용 하는 **위쪽**() 또는 **낮은**문자 필드 일관 된 대/소문자를 변환 하는 () 함수입니다. FoxPro 이상 버전 2.5, 대신 일반 데이터 정렬 순서 옵션을 지정 하 고 수 생략 된 **위쪽**() 변환 합니다.  
  
 컴퓨터 및.idx 파일을 만든 경우가 아닌 데이터 정렬 순서 옵션을 지정 하면 compact.idx는 항상 만들어집니다.  
  
 SET("COLLATE")를 사용 하 여 현재 데이터 정렬 시퀀스를 반환 합니다.  
  
 사용 하 여 데이터 원본에 대 한 데이터 정렬 순서를 지정할 수는 [ODBC Visual FoxPro 설정 대화 상자](../../odbc/microsoft/odbc-visual-foxpro-setup-dialog-box.md) 또는 사용 하 여 연결 문자열에 Collate 키워드를 사용 하 여 [SQLDriverConnect](../../odbc/microsoft/sqldriverconnect-visual-foxpro-odbc-driver.md)합니다. 다음 명령을 실행 하는 것과 같습니다.  
  
```  
SET COLLATE TO cSequenceName  
```  
  
## <a name="remarks"></a>주의  
 COLLATE 설정 하면 지원 되는 언어 중 하나에 대 한 악센트 부호가 있는 문자를 포함 하는 주문 테이블에 있습니다. COLLATE 설정의 설정을 변경 하면 이전에 열린된 인덱스의 데이터 정렬 순서 영향을 주지 않습니다. 자동으로 visual FoxPro를 유지 관리 기존 인덱스를 만드는 다양 한 유형의 인덱스, 같은 필드에 대해서도 유연성을 제공 합니다.  
  
 예를 들어 인덱스는 일반으로 설정 하는 한 부씩 설정 생성 되며 스페인어로 설정 하는 한 부씩 인쇄 설정을 나중에 변경, 인덱스 일반 데이터 정렬 순서를 유지 합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [ODBC Visual FoxPro 설치 대화 상자](../../odbc/microsoft/odbc-visual-foxpro-setup-dialog-box.md)
