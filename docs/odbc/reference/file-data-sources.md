---
title: 파일 데이터 소스 | 마이크로 소프트 문서
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 0661aa424a7a118b8b12f4bf8433987ff83bd788
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306654"
---
# <a name="file-data-sources"></a>파일 데이터 원본
*파일 데이터 원본은* 파일에 저장되며 연결 정보를 단일 사용자가 반복적으로 사용하거나 여러 사용자 간에 공유할 수 있습니다. 파일 데이터 원본을 사용하는 경우 드라이버 관리자는 .dsn 파일의 정보를 사용하여 데이터 원본에 연결합니다. 이 파일은 다른 파일처럼 조작할 수 있습니다. 파일 데이터 원본에는 컴퓨터 데이터 원본과 마찬가지로 데이터 원본 이름이 없으며 한 사용자 나 컴퓨터에 등록되지 않습니다.  
  
 .dsn 파일에는 **SQLDriverConnect** 함수를 호출하기 위해 빌드해야 하는 연결 문자열이 포함되어 있으므로 파일 데이터 원본은 연결 프로세스를 간소화합니다. .dsn 파일의 또 다른 장점은 모든 컴퓨터에 복사할 수 있으므로 적절한 드라이버가 설치되어 있는 한 많은 컴퓨터에서 동일한 데이터 원본을 사용할 수 있다는 것입니다. 파일 데이터 원본을 응용 프로그램에서 공유할 수도 있습니다. 공유 가능한 파일 데이터 원본을 네트워크에 배치하고 여러 응용 프로그램에서 동시에 사용할 수 있습니다.  
  
 .dsn 파일은 공유할 수 없습니다. 공유할 수 없는 .dsn 파일은 단일 컴퓨터에 상주하며 컴퓨터 데이터 원본을 가리킵니다. 공유 할 수없는 파일 데이터 원본은 주로 응용 프로그램이 파일 데이터 원본에서만 작동하도록 설계 될 수 있도록 기계 데이터 원본을 파일 데이터 원본으로 쉽게 변환 할 수 있도록 합니다. 드라이버 관리자는 공유할 수 없는 파일 데이터 원본에서 정보를 전송하면 .dsn 파일이 가리키는 컴퓨터 데이터 원본에 필요에 따라 연결됩니다.  
  
 파일 데이터 원본에 대한 자세한 내용은 [파일 데이터 원본 사용 또는](../../odbc/reference/develop-app/connecting-using-file-data-sources.md) [SQLDriverConnect](../../odbc/reference/syntax/sqldriverconnect-function.md) 함수 설명을 참조하십시오.
