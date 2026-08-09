export default async function handler(req, res) {
  if (req.method !== "POST") {
    return res.status(405).json({ error: "Method not allowed" });
  }

  const apiKey = process.env.OPENAI_API_KEY;
  if (!apiKey) {
    return res.status(500).json({ error: "OPENAI_API_KEY missing on server" });
  }

  const payload = req.body || {};
  const question = payload.question || "";

  const instructions = `
Tu es un coach de musculation au poids du corps, recomposition corporelle, récupération et cardio.
Tu analyses uniquement les données fournies par l'application.
Réponds en français, de façon concise, concrète et structurée.
Tu ne poses pas de diagnostic médical. Si une douleur >=4/10 est répétée, recommande de réduire/arrêter le mouvement concerné et de consulter un professionnel si elle persiste.
Ne recommande jamais une progression agressive en cas de douleur ou de fatigue élevée.

Pour un bilan hebdomadaire, utilise cette structure :
1. Résumé
2. Ce qui progresse
3. Ce qui bloque
4. Ajustement entraînement
5. Nutrition / perte de gras
6. Cardio / activité
7. Récupération
8. Priorités de la semaine prochaine

Ne fabrique aucune donnée absente.
`;

  const input = `Données de l'application :
${JSON.stringify(payload, null, 2)}

${question ? `Question de l'utilisateur : ${question}` : "Génère le bilan hebdomadaire complet."}`;

  try {
    const response = await fetch("https://api.openai.com/v1/responses", {
      method: "POST",
      headers: {
        "Authorization": `Bearer ${apiKey}`,
        "Content-Type": "application/json"
      },
      body: JSON.stringify({
        model: "gpt-5",
        instructions,
        input,
        store: false
      })
    });

    const data = await response.json();

    if (!response.ok) {
      return res.status(response.status).json({
        error: data?.error?.message || "OpenAI request failed"
      });
    }

    const text =
      data.output_text ||
      (data.output || [])
        .flatMap(item => item.content || [])
        .filter(c => c.type === "output_text")
        .map(c => c.text)
        .join("\n") ||
      "Aucune réponse textuelle.";

    return res.status(200).json({ text });
  } catch (error) {
    return res.status(500).json({ error: error.message || "Server error" });
  }
}
