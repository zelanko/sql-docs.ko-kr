---
title: 만들기 및 테이블 (텍스트 파일 드라이버) 열기 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- text file driver [ODBC], creating and opening tables
ms.assetid: e6a07dda-a665-4f5b-a8d6-9ff479700513
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ce901e6a8639c8a2caea6e55cbaa18fedb56f4a7
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47769101"
---
# <a name="creating-and-opening-tables-text-file-driver"></a>테이블 만들기 및 열기(텍스트 파일 드라이버)
텍스트 드라이버를 사용 하면 Odbcinst.ini에 지정 된 형식을 사용 하 여 새 테이블이 만들어집니다. 지정 하지 않으면 테이블이 CSVDELIMITED 형식으로 만들어집니다. 기본적으로 정수 열을 11 자로 기본 및 FLOAT 열 기본값 22 자입니다. 날짜 열 YYYY-월-일 형식을 사용 합니다. CHAR 및 LONGCHAR 열은 CREATE 문에서 지정 된 너비입니다.
