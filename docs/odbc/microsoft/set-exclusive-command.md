---
description: SET EXCLUSIVE 명령
title: SET EXCLUSIVE 명령 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SET EXCLUSIVE command [ODBC]
ms.assetid: d4fe12c5-7e8b-4d20-9ea4-2bcaffb271f2
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 413c9188decc9011c2816b692b1fb4b6112ec45b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88466355"
---
# <a name="set-exclusive-command"></a>SET EXCLUSIVE 명령
네트워크에서 단독으로 또는 공유 된 사용을 위해 테이블 파일을 열지 여부를 지정 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
SET EXCLUSIVE ON | OFF  
```  
  
## <a name="arguments"></a>인수  
 켜기  
 네트워크에 열려 있는 테이블의 접근성을 해당 테이블을 연 사용자에 게 제한 합니다. 네트워크의 다른 사용자가 테이블에 액세스할 수 없습니다. SET EXCLUSIVE를 사용 하면 다른 모든 사용자가 읽기 전용 액세스 권한을 갖지 못하게 됩니다.  
  
 OFF  
 (드라이버의 기본값입니다. Visual FoxPro의 기본값은 전역 데이터 세션에 대해 설정 되 고 개인 데이터 세션의 경우 해제 됩니다.) 네트워크에서 열린 테이블을 네트워크의 모든 사용자가 공유 하 고 수정할 수 있도록 허용 합니다.  
  
## <a name="remarks"></a>설명  
 SET EXCLUSIVE 설정을 변경 해도 이전에 열린 테이블의 상태는 변경 되지 않습니다. 예를 들어 SET EXCLUSIVE가 ON으로 설정 된 상태에서 테이블을 열고 EXCLUSIVE SET을 OFF로 변경 하면 테이블은 단독 사용 상태를 유지 합니다.  
  
## <a name="see-also"></a>관련 항목  
 [ODBC Visual FoxPro 설치 대화 상자](../../odbc/microsoft/odbc-visual-foxpro-setup-dialog-box.md)
