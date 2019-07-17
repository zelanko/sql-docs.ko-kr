---
title: 데이터 원본 파일 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data sources [ODBC], file
- file data sources [ODBC]
ms.assetid: db245c80-981a-4638-bd03-69d04bc67af0
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 9d27f168640b25652ed0fd40154ebfb677ef9300
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68068641"
---
# <a name="file-data-sources"></a>파일 데이터 원본
*데이터 원본 파일* 파일에 저장 되 고 단일 사용자가 반복적으로 사용 하거나 여러 사용자 간에 공유 연결 정보를 허용 합니다. 파일 데이터 소스를 사용 하면 드라이버 관리자.dsn 파일에 정보를 사용 하 여 데이터 원본에 연결을 만듭니다. 이 파일은 다른 파일 처럼 조작할 수 있습니다. 파일 데이터 원본이 없습니다 데이터 원본 이름, 컴퓨터 데이터 원본에는 모든 사용자 또는 컴퓨터에 등록 되어 있지 않습니다.  
  
 .Dsn 파일에 대 한 호출을 작성 해야 하는 연결 문자열을 포함 하기 때문에 파일 데이터 원본 연결 프로세스를 간소화 합니다 **SQLDriverConnect** 함수입니다. 다른.dsn 파일의 장점은 동일한 데이터 원본을 사용할 수 있도록 여러 컴퓨터에서으로 적절 한 드라이버가 설치 되어 있는 모든 컴퓨터에 복사할 수 있습니다. 파일 데이터 원본은 응용 프로그램에서 공유할 수도 있습니다. 공유할 수 있는 파일 데이터 원본 네트워크에 배치 하 고 여러 응용 프로그램에서 동시에 사용할 수 있습니다.  
  
 .Dsn 파일 또한 수 공유할 수 있는 합니다. 원본은.dsn 파일을 단일 컴퓨터에 있고 컴퓨터 데이터 원본을 가리킵니다. 공유할 수 없는 파일 데이터 원본 파일 데이터 원본에 데이터 원본은 쉽게 변환을 허용 하므로 파일 데이터 원본만 사용 하도록 응용 프로그램을 디자인할 수 있습니다를 주로 존재 합니다. 드라이버 관리자를 공유할 수 없는 파일 데이터 원본에 정보를 보내는 경우.dsn 파일을 가리키는 컴퓨터 데이터 원본에 필요에 따라 연결 합니다.  
  
 파일 데이터 원본에 대 한 자세한 내용은 참조 하세요. [를 사용 하 여 파일 데이터 원본에 연결](../../odbc/reference/develop-app/connecting-using-file-data-sources.md), 또는 [SQLDriverConnect](../../odbc/reference/syntax/sqldriverconnect-function.md) 함수 설명 합니다.
