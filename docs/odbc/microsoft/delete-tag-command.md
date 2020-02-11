---
title: 태그 삭제 명령 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 576e7e10d9d6f5c7e8616f57bde2dfed05503eae
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68112067"
---
# <a name="delete-tag-command"></a>DELETE TAG 명령
복합 인덱스 (cdx) 파일에서 태그 또는 태그를 제거 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
DELETE TAG TagName1 [OF CDXFileName1]  
   [, TagName2 [OF CDXFileName2]] ...  
  Or   
DELETE TAG ALL [OF CDXFileName]  
```  
  
## <a name="arguments"></a>인수  
 *TagName1* OF *CDXFileName1*[, *TagName2*[of *CDXFileName2*]] ...  
 복합 인덱스 파일에서 제거할 태그를 지정 합니다. 쉼표로 구분 된 태그 이름 목록을 포함 하 여 하나의 DELETE 태그를 사용 하 여 여러 태그를 삭제할 수 있습니다. 열려 있는 인덱스 파일에 동일한 이름을 가진 태그가 두 개 이상 있는 경우 *Cdxfilename*을 포함 하 여 특정 인덱스 파일에서 태그를 제거할 수 있습니다.  
  
 모든 [ *Cdxfilename*]  
 복합 인덱스 파일에서 모든 태그를 제거 합니다. 현재 테이블에 구조적 복합 인덱스 파일이 있는 경우 모든 태그가 인덱스 파일에서 제거 되 고, 인덱스 파일이 디스크에서 삭제 되 고, 테이블의 헤더에서 연결 된 구조적 복합 인덱스 파일이 있는지를 나타내는 플래그가 제거 됩니다. *Cdxfilename* 과 함께 모든 태그를 사용 하 여 구조적 복합 인덱스 파일이 아닌 열려 있는 복합 인덱스 파일에서 모든 태그를 제거 합니다.  
  
## <a name="remarks"></a>설명  
 인덱스를 사용 하 여 만든 복합 인덱스 파일에는 인덱스 항목에 해당 하는 태그가 포함 됩니다. 태그 삭제는 개방형 복합 인덱스 파일에서 태그 또는 태그를 제거 하는 데 사용 됩니다. 현재 작업 영역에 열려 있는 복합 인덱스 파일 에서만 태그를 삭제할 수 있습니다. 복합 인덱스 파일에서 모든 태그를 제거 하면 파일이 디스크에서 삭제 됩니다.  
  
 Visual FoxPro는 구조적 복합 인덱스 파일 (열려 있는 경우)에서 태그를 먼저 찾습니다. 태그가 구조적 복합 인덱스 파일에 없으면 Visual FoxPro는 다른 열린 복합 인덱스 파일에서 태그를 찾습니다.  
  
## <a name="see-also"></a>참고 항목  
 [INDEX 명령](../../odbc/microsoft/index-command.md)
