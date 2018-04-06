---
title: DELETE 태그 명령 | Microsoft Docs
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
- DELETE TAG command [ODBC]
ms.assetid: 4f4e1362-a5f3-4b15-8a3c-d4e96605f221
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: cf31107e21cee13d51046e43acc5c557cf20b9ee
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/21/2017
---
# <a name="delete-tag-command"></a>태그 명령 삭제
복합 인덱스 (.cdx) 파일에서 태그 또는 태그를 제거합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
DELETE TAG TagName1 [OF CDXFileName1]  
   [, TagName2 [OF CDXFileName2]] ...  
  Or   
DELETE TAG ALL [OF CDXFileName]  
```  
  
## <a name="arguments"></a>인수  
 *TagName1*OF *CDXFileName1*[, *TagName2*[OF *CDXFileName2*]]...  
 복합 인덱스 파일에서 제거할 태그를 지정 합니다. 쉼표로 구분 하 여 태그 이름의 목록을 포함 하 여 하나의 삭제 태그로 여러 태그를 삭제할 수 있습니다. 같은 이름의 두 개 이상의 태그 열린 인덱스 파일에 있으면에서 제거할 수 있습니다 태그 특정 인덱스 파일의 포함 하 여 *CDXFileName*합니다.  
  
 모든 [OF *CDXFileName*]  
 복합 인덱스 파일에서 모든 태그를 제거합니다. 현재 테이블에 구조적 복합 인덱스 파일이 있는 경우 모든 태그 인덱스 파일에서 제거 됩니다, 인덱스 파일은 디스크에서 삭제 및 관련된 구조적 복합 인덱스 파일의 존재를 나타내는 테이블의 머리글에 플래그가 제거 됩니다. OF 모두와 함께 사용 하 여 *CDXFileName* 구조적 복합 인덱스 파일이 아닌 다른 복합 인덱스 열린 파일에서 모든 태그를 제거 합니다.  
  
## <a name="remarks"></a>주의  
 복합 인덱스를 사용 하 여 만든 인덱스 파일, 인덱스 항목에 해당 하는 태그를 포함 합니다. 태그 삭제 열기 복합 인덱스 파일의 태그 또는 태그를 제거 하 사용 됩니다. 현재 작업 영역에 복합 인덱스 파일이 열려에서 태그만 삭제할 수 있습니다. 복합 인덱스 파일에서 모든 태그를 제거 하면 디스크에서 파일이 삭제 됩니다.  
  
 Visual FoxPro (열려 있으면) 태그 구조적 복합 인덱스 파일에 대 한 첫 번째를 찾습니다. 태그에에서 없는 경우 구조적 복합 인덱스 파일, Visual FoxPro 태그 다른 열린 복합 인덱스 파일에 대 한을 찾습니다.  
  
## <a name="see-also"></a>관련 항목:  
 [INDEX 명령](../../odbc/microsoft/index-command.md)
