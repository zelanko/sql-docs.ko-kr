---
title: 파일 데이터 원본을 | Microsoft Docs
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
- data sources [ODBC], file
- file data sources [ODBC]
ms.assetid: db245c80-981a-4638-bd03-69d04bc67af0
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 254e859c8533625cb34f7d867c62f26bea5cd04d
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="file-data-sources"></a>파일 데이터 원본
*파일 데이터 원본을* 파일에 저장 되 고 연결 정보를 단일 사용자가 반복적으로 사용 하거나 여러 사용자가 공유를 허용 합니다. 파일 데이터 원본을 사용 되는 경우 드라이버 관리자.dsn 파일에 정보를 사용 하 여 데이터 원본에 연결을 만듭니다. 이 파일은 다른 파일 처럼 조작할 수 있습니다. 파일 데이터 원본이 없는 데이터 원본 이름 처럼 컴퓨터 데이터 소스를 수행 하 고 하나의 사용자 또는 컴퓨터에 등록 되어 있지 않습니다.  
  
 .Dsn 파일에 대 한 호출을 작성 해야 하는 연결 문자열을 포함 하기 때문에 파일 데이터 원본 연결 프로세스를 간소화 된 **SQLDriverConnect** 함수입니다. .Dsn 파일의 또 다른 이점은 동일한 데이터 원본을 사용할 수 있도록 여러 컴퓨터에서 적절 한 드라이버가 설치 되어 있는으로 모든 컴퓨터에 복사 될 수 있습니다. 파일 데이터 원본은 응용 프로그램에서 공유할 수도 있습니다. 공유할 수 있는 파일 데이터 원본은 네트워크에 배치 하 고 동시에 여러 응용 프로그램에서 사용할 수 있습니다.  
  
 .Dsn 파일 또한 수 하지 공유할 수 있습니다. 공유할 수 없는.dsn 파일을 단일 컴퓨터에 상주 하며 컴퓨터 데이터 원본을 가리킵니다. 공유할 수 없는 파일 데이터 원본 파일 데이터 원본만 사용 하도록 응용 프로그램을 디자인할 수 있습니다 수 있도록 파일 데이터 원본에 데이터 원본은 쉬운 변환을 허용 하는 데 주로 존재 합니다. 드라이버 관리자를 공유할 수 없는 파일 데이터 원본에 정보를 보내는 경우.dsn 파일을 가리키는 데이터 원본 컴퓨터에 필요에 따라 연결 합니다.  
  
 파일 데이터 원본에 대 한 자세한 내용은 참조 [를 사용 하 여 파일 데이터 원본 연결](../../odbc/reference/develop-app/connecting-using-file-data-sources.md), 또는 [SQLDriverConnect](../../odbc/reference/syntax/sqldriverconnect-function.md) 함수 설명 합니다.
