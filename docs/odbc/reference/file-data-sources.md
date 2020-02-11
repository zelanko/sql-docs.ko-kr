---
title: 파일 데이터 원본 | Microsoft Docs
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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68068641"
---
# <a name="file-data-sources"></a>파일 데이터 원본
*파일 데이터 원본은* 파일에 저장 되 고 연결 정보는 단일 사용자가 반복적으로 사용 하거나 여러 사용자가 공유할 수 있습니다. 파일 데이터 원본을 사용할 때 드라이버 관리자는 dsn 파일의 정보를 사용 하 여 데이터 원본에 대 한 연결을 만듭니다. 이 파일은 다른 파일 처럼 조작할 수 있습니다. 파일 데이터 원본에는 컴퓨터 데이터 원본 처럼 데이터 원본 이름이 없고 한 사용자 또는 컴퓨터에 등록 되지 않습니다.  
  
 파일 데이터 원본은 **SQLDriverConnect** 함수를 호출 하기 위해 빌드해야 하는 연결 문자열을 dsn 파일에 포함 하기 때문에 연결 프로세스를 간소화 합니다. Dsn 파일의 또 다른 이점은 모든 컴퓨터에 복사할 수 있기 때문에 적절 한 드라이버를 설치한 경우에만 여러 컴퓨터에서 동일한 데이터 원본을 사용할 수 있다는 점입니다. 응용 프로그램 에서도 파일 데이터 소스를 공유할 수 있습니다. 공유 가능한 파일 데이터 원본은 네트워크에 배치 하 여 여러 응용 프로그램에서 동시에 사용할 수 있습니다.  
  
 Dsn 파일은 unshareable 수도 있습니다. Unshareable 파일은 단일 컴퓨터에 상주 하 고 컴퓨터 데이터 원본을 가리킵니다. Unshareable 파일 데이터 원본은 응용 프로그램이 파일 데이터 원본 에서만 작동 하도록 디자인 될 수 있도록 컴퓨터 데이터 원본을 파일 데이터 원본으로 쉽게 변환할 수 있도록 하는 데 주로 사용 됩니다. 드라이버 관리자는 unshareable 파일 데이터 원본으로 정보를 보낼 때 dsn 파일이 가리키는 컴퓨터 데이터 원본에 필요에 따라 연결 합니다.  
  
 파일 데이터 원본에 대 한 자세한 내용은 [파일 데이터 원본을 사용 하 여 연결](../../odbc/reference/develop-app/connecting-using-file-data-sources.md)또는 [SQLDriverConnect](../../odbc/reference/syntax/sqldriverconnect-function.md) 함수 설명을 참조 하세요.
