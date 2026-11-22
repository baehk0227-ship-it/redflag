export const handler = async (event) => {
  // POST 요청만 허용
  if (event.httpMethod !== "POST") {
    return { statusCode: 405, body: JSON.stringify({ error: "Method Not Allowed" }) };
  }

  const apiKey = process.env.GEMINI_API_KEY;
  if (!apiKey) {
    return {
      statusCode: 500,
      body: JSON.stringify({ error: "서버에 GEMINI_API_KEY가 설정되지 않았습니다." }),
    };
  }

  try {
    const { trait } = JSON.parse(event.body || "{}");
    if (!trait || !trait.trim()) {
      return { statusCode: 400, body: JSON.stringify({ error: "특징을 입력해 주세요." }) };
    }

    const prompt = `
당신은 재치 있고 현실적인 연애 상담가입니다.
사용자가 입력한 이성(또는 애인)의 특징을 보고, 애인으로서 괜찮은 사람인지(GREEN) 주의해야 할 사람인지(RED) 판독해 주세요.

입력된 특징: "${trait.trim()}"

반드시 아래 JSON 형식으로만 응답하세요:
{
  "flag": "GREEN" 또는 "RED",
  "score": 1부터 100 사이의 정수 (해당 플래그의 강도),
  "title": "재치 있고 임팩트 있는 한 줄 판정 (15자 내외)",
  "reason": "공감 가는 현실적인 이유 (2~3문장)",
  "advice": "실질적인 한 줄 연애 조언 (1문장)"
}
`;

    const response = await fetch(
      `https://generativelanguage.googleapis.com/v1beta/models/gemini-2.5-flash:generateContent?key=${apiKey}`,
      {
        method: "POST",
        headers: { "Content-Type": "application/json" },
        body: JSON.stringify({
          contents: [{ parts: [{ text: prompt }] }],
          generationConfig: {
            responseMimeType: "application/json",
            temperature: 0.8,
          },
        }),
      }
    );

    const data = await response.json();

    if (!response.ok) {
      throw new Error(data.error?.message || "Gemini API 호출 실패");
    }

    const resultText = data.candidates?.[0]?.content?.parts?.[0]?.text;
    const parsedResult = JSON.parse(resultText);

    return {
      statusCode: 200,
      headers: { "Content-Type": "application/json" },
      body: JSON.stringify(parsedResult),
    };
  } catch (error) {
    console.error("Judge Function Error:", error);
    return {
      statusCode: 500,
      body: JSON.stringify({ error: "판독 중 오류가 발생했습니다. 잠시 후 다시 시도해 주세요." }),
    };
  }
};
