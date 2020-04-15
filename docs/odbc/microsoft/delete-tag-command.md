---
title: 태그 삭제 명령 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- DELETE TAG command [ODBC]
ms.assetid: 4f4e1362-a5f3-4b15-8a3c-d4e96605f221
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 97ca5abca7e70f5dffdae9bf14ce64429fd203d5
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303544"
---
# <a name="delete-tag-command"></a>DELETE TAG 명령
복합 인덱스(.cdx) 파일에서 태그 또는 태그를 제거합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
DELETE TAG TagName1 [OF CDXFileName1]  
   [, TagName2 [OF CDXFileName2]] ...  
  Or   
DELETE TAG ALL [OF CDXFileName]  
```  
  
## <a name="arguments"></a>인수  
 *태그네임1* *OF CDXFileName1*[, *태그네임2* *[CDXFileName2]]*...  
 복합 인덱스 파일에서 제거할 태그를 지정합니다. 쉼표로 구분된 태그 이름 목록을 포함하여 하나의 DELETE TAG로 여러 태그를 삭제할 수 있습니다. 이름이 같은 태그가 열려 있는 인덱스 파일에 있는 경우 *OF CDXFileName*을 포함하여 특정 인덱스 파일에서 태그를 제거할 수 있습니다.  
  
 모든 *[CDXFileName]*  
 복합 인덱스 파일에서 모든 태그를 제거합니다. 현재 테이블에 구조 복합 인덱스 파일이 있는 경우 모든 태그가 인덱스 파일에서 제거되고 인덱스 파일이 디스크에서 삭제되고 테이블 헤더의 플래그가 연관된 구조 복합 인덱스 파일이 없음을 나타냅니다. *OF CDXFileName을* 사용하여 구조 복합 인덱스 파일이 아닌 열린 복합 인덱스 파일에서 모든 태그를 제거합니다.  
  
## <a name="remarks"></a>설명  
 INDEX로 만든 복합 인덱스 파일에는 인덱스 항목에 해당하는 태그가 포함됩니다. DELETE 태그는 열린 복합 인덱스 파일에서 태그 또는 태그를 제거하는 데 사용됩니다. 현재 작업 영역에서 열린 복합 인덱스 파일에서 태그만 삭제할 수 있습니다. 복합 인덱스 파일에서 모든 태그를 제거하면 파일이 디스크에서 삭제됩니다.  
  
 Visual FoxPro는 구조 복합 인덱스 파일(열려 있는 경우)에서 태그를 먼저 찾습니다. 태그가 구조 복합 인덱스 파일에 없는 경우 Visual FoxPro는 열려 있는 다른 복합 인덱스 파일에서 태그를 찾습니다.  
  
## <a name="see-also"></a>참고 항목  
 [INDEX 명령](../../odbc/microsoft/index-command.md)
