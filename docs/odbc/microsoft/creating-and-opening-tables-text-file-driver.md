---
title: 테이블 만들기 및 열기(텍스트 파일 드라이버) | 마이크로 소프트 문서
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ae13312299f131d1957557db28bbe4db0bf7b4c7
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81280923"
---
# <a name="creating-and-opening-tables-text-file-driver"></a>테이블 만들기 및 열기(텍스트 파일 드라이버)
텍스트 드라이버를 사용하면 Odbcinst.ini에 지정된 형식을 사용하여 새 테이블이 만들어집니다. 지정하지 않으면 테이블이 CSVDELIMITED 형식으로 만들어집니다. 기본적으로 INTEGER 열은 기본값으로 11자, FLOAT 열은 기본적으로 22자로 설정됩니다. DATE 열은 YYYY-MM-DD 형식을 사용합니다. CHAR 및 LONGCHAR 열은 CREATE 문에 지정된 너비입니다.
