---
title: 부록-1 (AccessToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 00665e16-2990-4bfc-8e17-d97ca9fb4999
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: ca084ec1849ab22940bb1617476637c105e90609
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68115026"
---
# <a name="appendix---1-accesstosql"></a>부록-1 (AccessToSQL)
SSMA 콘솔 명령줄 옵션의 빠른 보기:  
  
|Sl. 아니요.|스위치|필수 여부|Switch 인수|허용 되는 값|  
|-----------|----------|-------------|-------------------|--------------------|  
|1|-s/스크립트|yes|scriptfile|올바른 XML 파일 이름입니다.<br /><br />콘솔 스크립트 정의 파일입니다.|  
|2|-v/변수|예|variablevaluefile|올바른 XML 파일 이름입니다. 스크립트 파일에서 변수를 사용 하는 경우이 파일을 지정 해야 합니다.|  
|3|-c/serverconnection|예|serverconnectionfile|올바른 XML 파일 이름입니다. 이 파일에는 서버 연결 정보가 포함 되어 있습니다.|  
|4|-x/xmloutput|예|xmloutputfile|이 옵션은 XML 형식의 콘솔 출력을 나타냅니다. 이 옵션을 지정 하지 않으면 기본 출력은 텍스트 형식입니다.<br /><br />Xmloutputfile을 지정 하지 않으면 XML 출력은 STDOUT으로 전송 됩니다.<br /><br />Xmloutputfile은 콘솔 출력이 XML 형식으로 작성 되는 파일의 이름입니다.|  
|5|-l/로그|예|logfile|유효한 파일 이름입니다.|  
|6|-e/projectenvironment|예|project환경 폴더|SSMA 프로젝트 환경 파일이 포함 된 올바른 폴더 이름입니다.|  
|7|-p/securepassword|예|-a/add {<server_id> [,... n] &#124; 모든}-c&#124;serverconnection <서버-연결 파일> [-v&#124;변수 <변수-값-파일>] [-o/overwrite]<br /><br />또는<br /><br />-a/add {<server_id> [,... n] &#124; 모든} s&#124;스크립트 <스크립트 파일> [-v&#124;변수 <변수-값-파일>] [-o/overwrite]<br /><br />-r/remove {<server_id> [, ... n] &#124; all}<br /><br />-l/list<br /><br />-e/내보내기 {<서버 id> [, ... n] &#124; 모든} <암호화 된 암호 파일><br /><br />-i/import {<server-id> [, ... n] &#124; 모든} <암호화 된 암호 파일>|지정 된 경우이 옵션은 다른 옵션과 함께 사용할 수 없습니다.<br /><br />서버 id: {string} 서버에 대해 제공 된 고유 ID<br /><br />서버 연결-파일: 서버 정의 파일 (serverconnectionfile 또는 scriptfile).<br /><br />변수-값-파일: 변수 정의 파일이 며 서버 연결 파일에 사용 됩니다.<br /><br />암호화 된 암호-파일: 사용자 지정 암호문을 사용 하 여 암호화 된 서버 암호 파일입니다.|  
|8|-?|예|해당 없음|해당 없음|  
  
## <a name="see-also"></a>참고 항목  
[SSMA 콘솔 실행 (Access)](https://msdn.microsoft.com/aa1bf665-8dc0-4259-b36f-46ae67197a43)  
  
