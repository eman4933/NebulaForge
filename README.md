// ChatbotUI.jsx (React)
import { useState } from 'react';

export default function ChatbotUI() {
  const [msgs, setMsgs] = useState([]);
  const [txt, setTxt] = useState('');

  const send = () => {
    setMsgs([...msgs, { from: 'You', text: txt }, { from: 'Bot', text: `Echo: ${txt}` }]);
    setTxt('');
  };

  return (
    <div>
      <div>{msgs.map((m, i) => <div key={i}><b>{m.from}:</b> {m.text}</div>)}</div>
      <input value={txt} onChange={e => setTxt(e.target.value)} onKeyDown={e => e.key === 'Enter' && send()} />
      <button onClick={send}>Send</button>
    </div>
  );
}
