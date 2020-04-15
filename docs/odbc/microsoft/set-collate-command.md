---
title: 콜레이트 커맨드 설정 | 마이크로 소프트 문서
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
ms.openlocfilehash: 4a9c1dfd59c00ad0ac0b7bd8b8f1cdfccc84d9b3
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300893"
---
# <a name="set-collate-command"></a>SET COLLATE 명령
후속 인덱싱 및 정렬 작업에서 문자 필드에 대한 데이터 정렬 시퀀스를 지정합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
SET COLLATE TO cSequenceName  
```  
  
## <a name="arguments"></a>인수  
 *c시퀀스 이름*  
 데이터 정렬 시퀀스를 지정합니다. 사용 가능한 데이터 정렬 시퀀스 옵션은 다음 표에 설명되어 있습니다.  
  
|옵션|언어|  
|-------------|--------------|  
|네덜란드어|네덜란드어|  
|GENERAL|영어, 프랑스어, 독일어, 현대 스페인어, 포르투갈어 및 기타 서유럽 언어|  
|독일어|독일어 전화 번호부 주문(DIN)|  
|아이슬란드|아이슬란드어|  
|기계|컴퓨터(이전 FoxPro 버전의 기본 데이터 정렬 시퀀스)|  
|노르단 (주)|노르웨이어, 덴마크어|  
|스페인어|전통 스페인어|  
|스웨핀 (미국)|스웨덴어, 핀란드어|  
|유니크WT|고유 무게|  
  
> [!NOTE]  
>  스페인어 옵션을 지정할 때 *ch는* *c와* *d*간에 정렬되고 *l과* *m*사이에서 정렬되는 단일 문자입니다. *l*  
  
 데이터 정렬 시퀀스 옵션을 리터럴 문자 문자열로 지정하는 경우 따옴표로 옵션을 동봉해야 합니다.  
  
```  
SET COLLATE TO "SWEFIN"  
```  
  
 MACHINE은 기본 데이터 정렬 시퀀스 옵션이며 Xbase 사용자가 익숙한 시퀀스입니다. 문자는 현재 코드 페이지에 표시되는 순서대로 정렬됩니다.  
  
 일반은 미국 및 서유럽 사용자에게 더 바람직할 수 있습니다. 문자는 현재 코드 페이지에 표시되는 순서대로 정렬됩니다. 2.5보다 이전의 FoxPro 버전에서는 문자 필드를 일관된 대/소문자로 변환하기 위해 **UPPER**() 또는 **LOWER()** 함수를 사용하여 인덱스가 만들어졌을 수 있습니다. 2.5 이상 FoxPro 버전에서는 일반 데이터 정렬 시퀀스 옵션을 대신 지정하고 **UPPER**() 변환을 생략할 수 있습니다.  
  
 MACHINE 이외의 데이터 정렬 시퀀스 옵션을 지정하고 .idx 파일을 만드는 경우 항상 압축 .idx가 만들어집니다.  
  
 SET("COLLATE")을 사용하여 현재 데이터 정렬 시퀀스를 반환합니다.  
  
 [ODBC Visual FoxPro 설치 대화 상자또는](../../odbc/microsoft/odbc-visual-foxpro-setup-dialog-box.md) [SQLDriverConnect를](../../odbc/microsoft/sqldriverconnect-visual-foxpro-odbc-driver.md)사용하여 연결 문자열에 Collate 키워드를 사용하여 데이터 원본에 대한 데이터 원본의 정렬 시퀀스를 지정할 수 있습니다. 이는 다음 명령을 실행한 것과 동일합니다.  
  
```  
SET COLLATE TO cSequenceName  
```  
  
## <a name="remarks"></a>설명  
 SET COLLATE를 사용하면 지원되는 언어에 대해 악센트 있는 문자가 포함된 테이블을 주문할 수 있습니다. SET COLLATE의 설정을 변경해도 이전에 열린 인덱스의 정렬 순서에는 영향을 주지 않습니다. Visual FoxPro는 기존 인덱스를 자동으로 유지 관리하여 동일한 필드에 대해서도 다양한 유형의 인덱스를 만들 수 있는 유연성을 제공합니다.  
  
 예를 들어 SET COLLATE를 일반으로 설정하고 SET COLLATE 설정이 나중에 스페인어로 변경된 인덱스를 사용하여 인덱스를 만들면 인덱스는 일반 데이터 정렬 시퀀스를 유지합니다.  
  
## <a name="see-also"></a>참고 항목  
 [ODBC Visual FoxPro 설치 대화 상자](../../odbc/microsoft/odbc-visual-foxpro-setup-dialog-box.md)
