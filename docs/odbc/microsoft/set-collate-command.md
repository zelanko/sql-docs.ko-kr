---
title: SET COLLATE 명령 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- set collate command [ODBC]
ms.assetid: 00efbcd4-fea8-4061-86a5-82de413cb753
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 372d3b2df79d66084f5599b4ac098b8c273ee78a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63127838"
---
# <a name="set-collate-command"></a>SET COLLATE 명령
후속 인덱싱 및 정렬 작업에서 문자 필드에 대 한 데이터 정렬 순서를 지정합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
SET COLLATE TO cSequenceName  
```  
  
## <a name="arguments"></a>인수  
 *cSequenceName*  
 데이터 정렬 순서를 지정합니다. 사용 가능한 데이터 정렬 순서 옵션은 다음과에서 같습니다.  
  
|변수|언어|  
|-------------|--------------|  
|네덜란드어|네덜란드어|  
|GENERAL|영어, 프랑스어, 독일어, 현대 스페인어, 포르투갈어, 서 부 유럽 언어|  
|독일어|독일어 전화 번호부 순서 (DIN)|  
|아이슬란드|아이슬란드어|  
|컴퓨터|컴퓨터 (FoxPro 버전에 대 한 기본 데이터 정렬 순서)|  
|NORDAN|노르웨이어, 덴마크어|  
|스페인어|전통 스페인어|  
|SWEFIN|스웨덴어 핀란드어|  
|UNIQWT|고유 가중치|  
  
> [!NOTE]  
>  스페인어 옵션을 지정 하는 경우 *ch* 간에 정렬 하는 단일 문자입니다 *c* 하 고 *d*, 및 *ll* 간에 정렬  *l* 하 고 *m*합니다.  
  
 리터럴 문자열로 데이터 정렬 순서 옵션을 지정 하는 경우에 옵션을 따옴표로 묶습니다 야 합니다.  
  
```  
SET COLLATE TO "SWEFIN"  
```  
  
 컴퓨터의 기본 데이터 정렬 순서 옵션이 이며 시퀀스 Xbase 사용자를 잘 알고 있습니다. 문자는 현재 코드 페이지에 나타나는 대로 정렬 됩니다.  
  
 일반 미국 및 유럽 서 부 사용자에 대 한 선호 될 수 있습니다. 문자는 현재 코드 페이지에 나타나는 대로 정렬 됩니다. FoxPro 버전에서 2.5에서는 이전 인덱스 만들어졌을 수를 사용 하는 **위쪽**() 또는 **낮은**문자 필드는 일관 된 대/소문자를 변환할 () 함수입니다. FoxPro 버전 2.5 이상에서는 대신 일반 데이터 정렬 순서 옵션을 지정 하 고 수 생략 합니다 **위**() 변환 합니다.  
  
 컴퓨터 및.idx 파일을 만든 경우가 아닌 데이터 정렬 순서 옵션을 지정 하는 경우에 compact.idx 항상 만들어집니다.  
  
 SET("COLLATE")를 사용 하 여 현재 데이터 정렬 시퀀스를 반환 합니다.  
  
 사용 하 여 데이터 원본에 대 한 정렬 순서를 지정할 수 있습니다 합니다 [ODBC Visual FoxPro 설치 대화 상자가](../../odbc/microsoft/odbc-visual-foxpro-setup-dialog-box.md) 또는 사용 하 여 연결 문자열에 Collate 키워드를 사용 하 여 [SQLDriverConnect](../../odbc/microsoft/sqldriverconnect-visual-foxpro-odbc-driver.md)합니다. 다음 명령을 실행 하는 것과 동일 합니다.  
  
```  
SET COLLATE TO cSequenceName  
```  
  
## <a name="remarks"></a>Remarks  
 데이터 정렬 설정 하면 지원 되는 언어에 대 한 악센트 부호가 있는 문자를 포함 하는 주문 테이블. 데이터 정렬 설정의 설정 변경 이전에 열린된 인덱스의 정렬 순서에 영향을 주지 않습니다. Visual FoxPro 자동으로 기존 인덱스 유지 다양 한 유형의 동일한 필드에 대해서도 인덱스를 만드는 유연성을 제공 합니다.  
  
 예를 들어 일반으로 설정 하는 데이터 정렬 설정으로 인덱스를 만들 경우 스페인어로 설정 하는 한 부씩 인쇄 설정을 나중에 변경 인덱스의 일반적인 데이터 정렬 순서를 유지 합니다.  
  
## <a name="see-also"></a>관련 항목  
 [ODBC Visual FoxPro 설치 대화 상자](../../odbc/microsoft/odbc-visual-foxpro-setup-dialog-box.md)
