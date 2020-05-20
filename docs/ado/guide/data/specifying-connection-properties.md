---
title: 연결 속성 지정 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- connection properties [ADO]
- connections [ADO]
ms.assetid: 49456201-b085-4851-9686-e814136b07be
author: rothja
ms.author: jroth
ms.openlocfilehash: 6fee9745bca206f00603b32a6c4cd29faab34eca
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/04/2020
ms.locfileid: "82760839"
---
# <a name="specifying-connection-properties"></a>연결 속성 지정
연결을 열기 전에 **연결 개체의** 속성을 설정 하 여 연결 [문자열](../../../ado/guide/data/creating-a-connection-string.md) 에 지정 된 많은 정보를 제공할 수 있습니다. 예를 들어 다음 코드를 사용 하 여 [연결 문자열을 만드는 데](../../../ado/guide/data/creating-a-connection-string.md) 설명 된 연결 문자열과 동일한 효과를 달성할 수 있습니다.  
  
```  
With objConn  
.Provider = "SQLOLEDB"  
.Properties("Data Source") = "MySqlServer"  
   .Properties("Integrated Security") = "SSPI"  
.Open  
.DefaultDatabase = "Northwind"  
End With  
```  
  
 DefaultDatabase는 연결을 연 후에만 설정 됩니다.  
  
> [!NOTE]
>  ADO에서는 암호가 작은따옴표로 묶여 있지 않으면 세미콜론 (";")이 포함 된 암호를 사용 하면 안 됩니다.
