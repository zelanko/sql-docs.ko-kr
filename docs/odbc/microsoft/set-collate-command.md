---
description: SET COLLATE 명령
title: COLLATE 명령 설정 | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 5ca796da60adf0c432b5bbd80065e58563664bc5
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88466385"
---
# <a name="set-collate-command"></a>SET COLLATE 명령
후속 인덱싱 및 정렬 작업에서 문자 필드에 대 한 데이터 정렬 시퀀스를 지정 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
SET COLLATE TO cSequenceName  
```  
  
## <a name="arguments"></a>인수  
 *cSequenceName*  
 데이터 정렬 시퀀스를 지정 합니다. 다음 표에서는 사용 가능한 데이터 정렬 순서 옵션에 대해 설명 합니다.  
  
|옵션|Language|  
|-------------|--------------|  
|네덜란드어|네덜란드어|  
|GENERAL|영어, 프랑스어, 독일어, 최신 스페인어, 포르투갈어 및 기타 서유럽어 언어|  
|독일어|독일어 전화 번호부 주문 (DIN)|  
|아이슬란드|아이슬란드어|  
|컴퓨터|Machine (이전 FoxPro 버전의 기본 데이터 정렬 순서)|  
|가 나 DAN|노르웨이어, 덴마크어|  
|스페인어|전통 스페인어|  
|SWEFIN|스웨덴어, 핀란드어|  
|UNIQWT|고유 가중치|  
  
> [!NOTE]  
>  스페인어 옵션을 지정 하면 *ch* 는 *c* 와 *d*사이를 정렬 하는 단일 문자 이며 *ll* 은 *l* 과 *m*사이를 정렬 합니다.  
  
 데이터 정렬 시퀀스 옵션을 리터럴 문자열로 지정 하는 경우 옵션을 큰따옴표로 묶어야 합니다.  
  
```  
SET COLLATE TO "SWEFIN"  
```  
  
 MACHINE은 기본 데이터 정렬 시퀀스 옵션이 며 사용자에 게 친숙 한 시퀀스 Xbase. 문자는 현재 코드 페이지에 표시 되는 순서 대로 정렬 됩니다.  
  
 일반은 미국 및 서유럽 사용자에 게 더 적합할 수 있습니다. 문자는 현재 코드 페이지에 표시 되는 순서 대로 정렬 됩니다. 2.5 이전의 FoxPro 버전에서 문자 필드를 일관 된 대/소문자로 변환 하기 위해 **UPPER**() 또는 **LOWER**() 함수를 사용 하 여 인덱스를 만들었을 수 있습니다. 2.5 이후의 FoxPro 버전에서는 대신 GENERAL collation sequence 옵션을 지정 하 고 **UPPER**() 변환을 생략할 수 있습니다.  
  
 컴퓨터 이외의 데이터 정렬 시퀀스 옵션을 지정 하 고 idx 파일을 만드는 경우에는 항상 압축 된 idx가 만들어집니다.  
  
 SET ("COLLATE")를 사용 하 여 현재 데이터 정렬 시퀀스를 반환 합니다.  
  
 [ODBC Visual FoxPro 설치 대화 상자](../../odbc/microsoft/odbc-visual-foxpro-setup-dialog-box.md) 를 사용 하거나 [SQLDriverConnect](../../odbc/microsoft/sqldriverconnect-visual-foxpro-odbc-driver.md)를 사용 하 여 연결 문자열에서 Collate 키워드를 사용 하 여 데이터 원본에 대 한 데이터 정렬 순서를 지정할 수 있습니다. 다음 명령을 실행 하는 것과 같습니다.  
  
```  
SET COLLATE TO cSequenceName  
```  
  
## <a name="remarks"></a>설명  
 COLLATE를 설정 하면 지원 되는 모든 언어에 대해 악센트가 있는 문자가 포함 된 테이블의 순서를 지정할 수 있습니다. SET COLLATE 설정을 변경 해도 이전에 열린 인덱스의 데이터 정렬 순서에는 영향을 주지 않습니다. Visual FoxPro는 기존 인덱스를 자동으로 유지 하 여 동일한 필드에 대해서도 다양 한 유형의 인덱스를 유연 하 게 만들 수 있습니다.  
  
 예를 들어 COLLATE set을 일반으로 설정 하 여 인덱스를 만들고 COLLATE 설정 설정이 나중에 스페인어로 변경 되는 경우 인덱스는 일반 데이터 정렬 시퀀스를 유지 합니다.  
  
## <a name="see-also"></a>관련 항목  
 [ODBC Visual FoxPro 설치 대화 상자](../../odbc/microsoft/odbc-visual-foxpro-setup-dialog-box.md)
