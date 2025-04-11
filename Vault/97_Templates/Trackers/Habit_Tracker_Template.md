<%-* const prompt = ["Weight Log", "Wake up Time", "Sleep Time", "Diet Score", "Exercise Duration"]
type = await tp.system.suggester(prompt, prompt) %>
<%-* if (type === "Weight Log"){%>⚖ [WeightUpdate:: <%tp.file.cursor()%>]
<%-*} else if (type === "Wake up Time"){%>🌞 [offBed:: <%tp.date.now("HH:mm")%>]
<%-*} else if (type === "Sleep Time"){%>🌙 [onBed:: <%tp.date.now("HH:mm")%>]
<%-*} else if (type === "Diet Score"){%>🍗 [diet:: <%tp.file.cursor()%>]
<%-*} else if (type === "Exercise Duration"){%>🏋️‍♂️ [exercise:: <%tp.file.cursor()%>]
<%-*} %>
