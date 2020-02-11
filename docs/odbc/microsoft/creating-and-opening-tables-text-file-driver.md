---
title: 테이블 만들기 및 열기 (텍스트 파일 드라이버) | Microsoft Docs
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
ms.openlocfilehash: b36c02d772682088a799cfca66f5bbf3e169a67f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68096540"
---
# <a name="creating-and-opening-tables-text-file-driver"></a>테이블 만들기 및 열기(텍스트 파일 드라이버)
텍스트 드라이버를 사용 하는 경우 Odbcinst.ini에 지정 된 형식을 사용 하 여 새 테이블을 만듭니다. 지정 하지 않으면 테이블은 CSVDELIMITED 형식으로 만들어집니다. 기본적으로 정수 열 기본값은 11 자, FLOAT 열은 기본적으로 22 자입니다. 날짜 열은 YYYY-MM-DD 형식을 사용 합니다. CHAR 및 no CHAR 열은 CREATE 문에 지정 된 너비입니다.
