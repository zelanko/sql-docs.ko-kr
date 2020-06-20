---
title: SQLFreeHandle | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- SQLFreeHandle function
ms.assetid: d374e5c8-ed35-43bf-8dd6-c37e38d9b5f1
author: rothja
ms.author: jroth
ms.openlocfilehash: f51f031bec05715e0345507278113f4f16179a77
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85022350"
---
# <a name="sqlfreehandle"></a>SQLFreeHandle
  수동 커밋 모드에서 트랜잭션이 열려 있을 때 문 핸들에 대해 **SQLFreeHandle** 을 호출하면 보류 중인 변경 내용이 데이터베이스에 롤백됩니다. 문 핸들에 대해 **SQLFreeHandle** 을 호출하면 항상 열려 있는 모든 커서가 닫히고 보류 중인 결과가 삭제되어 문 핸들에 연결된 모든 리소스가 해제됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQLFreeHandle 함수](https://go.microsoft.com/fwlink/?LinkId=59345)   
 [ODBC API 구현 정보](odbc-api-implementation-details.md)  
  
  
