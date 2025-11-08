# Social-Prompt-Generator
import React, { useState } from "react";
import { FaYoutube, FaFacebook, FaInstagram, FaTiktok } from "react-icons/fa";

const platforms = {
  youtube: { color: "bg-red-500", logo: <FaYoutube size={30} /> },
  facebook: { color: "bg-blue-600", logo: <FaFacebook size={30} /> },
  instagram: { color: "bg-gradient-to-r from-pink-500 via-purple-500 to-yellow-400", logo: <FaInstagram size={30} /> },
  tiktok: { color: "bg-black", logo: <FaTiktok size={30} /> },
};

const languages = [
  "English", "Urdu", "Hindi", "Arabic", "Spanish",
  "French", "German", "Chinese", "Japanese", "Turkish"
];

function App() {
  const [platform, setPlatform] = useState("youtube");
  const [language, setLanguage] = useState("English");
  const [prompt, setPrompt] = useState("");
  const [title, setTitle] = useState("");
  const [description, setDescription] = useState("");
  const [tags, setTags] = useState("");

  const generateContent = () => {
    // Example generation logic (replace with AI API call if needed)
    setTitle(`${prompt} - ${platform.toUpperCase()} Title`);
    setDescription(`${prompt} description in ${language}`);
    setTags(`#${platform} #${prompt.replace(/\s+/g,"")} #${language}`);
  };

  return (
    <div className="min-h-screen flex flex-col items-center justify-center p-5">
      <h1 className="text-3xl font-bold mb-5">Social Prompt Generator</h1>

      <div className="flex gap-3 mb-5">
        {Object.keys(platforms).map(p => (
          <button
            key={p}
            className={`p-3 rounded ${platform === p ? "ring-4 ring-offset-2 ring-indigo-500" : ""}`}
            onClick={() => setPlatform(p)}
          >
            {platforms[p].logo}
          </button>
        ))}
      </div>

      <div className="mb-5">
        <select
          value={language}
          onChange={(e) => setLanguage(e.target.value)}
          className="border p-2 rounded"
        >
          {languages.map(lang => <option key={lang} value={lang}>{lang}</option>)}
        </select>
      </div>

      <textarea
        className="border p-3 w-full max-w-lg rounded mb-5"
        rows="3"
        placeholder="Enter your prompt here..."
        value={prompt}
        onChange={(e) => setPrompt(e.target.value)}
      />

      <button
        className={`text-white p-3 rounded mb-5 w-full max-w-lg ${platforms[platform].color}`}
        onClick={generateContent}
      >
        Generate
      </button>

      {title && (
        <div className="max-w-lg w-full p-4 border rounded space-y-2">
          <h2 className="font-bold">Title:</h2>
          <p>{title}</p>

          <h2 className="font-bold">Description:</h2>
          <p>{description}</p>

          <h2 className="font-bold">Tags:</h2>
          <p>{tags}</p>
        </div>
      )}
    </div>
  );
}

export default App;

