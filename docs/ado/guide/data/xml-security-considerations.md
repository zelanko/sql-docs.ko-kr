---
title: XML 보안 고려 사항 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- XML security in ADO
ms.assetid: fadbd38e-6e7b-4b81-96ea-85169c664374
author: rothja
ms.author: jroth
ms.openlocfilehash: ab98aaf7bb2a0f4887df5a1c2276fe0df8862972
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/04/2020
ms.locfileid: "82748221"
---
# <a name="xml-security-considerations"></a>XML 보안 고려 사항
레코드 집합 개체에 대 한 ADO Save 및 Open 메서드는 Internet Explorer에서 실행 되는 안전한 작업으로 간주 되지 않습니다. 따라서 브라우저에서 호스팅되는 응용 프로그램이 나 컨트롤에서 실행 되는 스크립트 코드에서 이러한 메서드를 사용 하는 경우 브라우저의 보안 구성은 동작에 영향을 미칠 수 있습니다.  
  
 Internet Explorer 5는 인터넷 영역에서 기본적으로 이러한 작업에 대 한 보안 제한을 제공 합니다. 이 구성에서 레코드 집합은 클라이언트의 로컬 파일 시스템에 액세스할 수 없거나, 해당 페이지가 다운로드 된 서버 도메인의 외부에 있는 모든 데이터 원본에 액세스할 수 없습니다. 특히, 브라우저 호스트 내에서 실행 하는 경우 페이지가 다운로드 된 서버와 동일한 서버에 있는 경우에만 레코드 집합을 파일에 다시 저장할 수 있습니다. 마찬가지로 해당 파일이 페이지가 다운로드 된 서버와 동일한 서버에 있는 경우에만 파일에서 레코드 집합을 로드 하 여 열 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [XML 형식으로 레코드 유지](../../../ado/guide/data/persisting-records-in-xml-format.md)
