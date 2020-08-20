---
description: UPDATE 문 제한 사항
title: 문 제약 조건 업데이트 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- UPDATE statement limitations [ODBC]
- ODBC SQL grammar, UPDATE statement limitations
ms.assetid: 14700aac-e135-4dc0-9138-4b01224461d5
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b7c1ea2e5e9d887005084cdb5454dcf9b5e8fa24
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88471402"
---
# <a name="update-statement-limitations"></a>UPDATE 문 제한 사항
Paradox 드라이버에서 테이블을 업데이트 하려면 테이블에 고유 인덱스 (Paradox 기본 키)가 있어야 합니다. Borland 데이터베이스 엔진를 구현 하지 않고 Paradox 드라이버를 사용 하는 경우에는 Paradox 테이블을 업데이트할 수 없습니다.  
  
 텍스트 드라이버에서 지원 되지 않습니다.  
  
 Microsoft Excel 드라이버를 사용 하는 경우 값을 업데이트할 수 있지만 Microsoft Excel 스프레드시트를 기반으로 하는 테이블에서 행을 삭제할 수 없습니다. 따라서 UPDATE 문은 Microsoft Excel 드라이버에서 공식적으로 지원 되는 것으로 간주 되지 않습니다. INSERT 문만 지원 되는 것으로 간주 됩니다.
