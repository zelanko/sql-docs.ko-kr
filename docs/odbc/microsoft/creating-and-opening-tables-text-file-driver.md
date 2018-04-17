---
title: 만들기 및 열기 테이블 (텍스트 파일 드라이버) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
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
- text file driver [ODBC], creating and opening tables
ms.assetid: e6a07dda-a665-4f5b-a8d6-9ff479700513
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 374a234f7c0f9eecc119e36d7dd4305a32745786
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="creating-and-opening-tables-text-file-driver"></a>만들기 및 테이블 (텍스트 파일 드라이버) 열기
텍스트 드라이버를 사용 하면 Odbcinst.ini에 지정 된 형식을 사용 하 여 새 테이블이 만들어집니다. 지정 하지 않으면 테이블이 CSVDELIMITED 형식으로 만들어집니다. 기본적으로 정수 열 11 자로 기본 하 및 FLOAT 열 22 자가 하 기본 키를 누릅니다. 날짜 열에는 YYYY-월-일 형식을 사용합니다. CHAR 및 LONGCHAR 열 만들기 문에 지정 된 너비는입니다.
