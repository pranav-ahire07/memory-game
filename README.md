# Memory Match Game

A classic card-matching memory game built with React. Flip two cards at a time, find matching fruit pairs, and try to clear the board in as few moves as possible.

## Features

- 8 pairs of cards (16 total), shuffled into a new layout on every game start
- Flip-and-match logic: two mismatched cards flip back automatically
- Score and move counter
- Game-complete detection once all pairs are matched
- Restart/reset support via `initializeGame`
- Game logic separated into a reusable custom hook (`useGameLogic`)

## Tech Stack

- React (functional components, hooks)
- Custom hook for game state (`useState`, no external state library)

## Getting Started

Clone the repo and install dependencies:

\`\`\`bash
git clone https://github.com/<your-username>/memory-game.git
cd memory-game
npm install
\`\`\`

Run the development server:

\`\`\`bash
npm start
\`\`\`

Open [http://localhost:3000](http://localhost:3000) in your browser.

## Project Structure

\`\`\`
src/
├── components/
│   ├── Card.js          # Single flippable card
│   └── GameHeader.js     # Displays score and move count
├── hooks/
│   └── useGameLogic.js   # All game state and logic (shuffle, flip, match, score)
└── App.js
\`\`\`

## How It Works

- Cards are shuffled using a Fisher–Yates shuffle on game start (via a lazy `useState` initializer, so it only runs once on mount — not an effect).
- Clicking a card flips it, unless the board is locked (two cards already face-up and being checked) or the card is already flipped/matched.
- When two cards are flipped:
  - If they match, both are marked `isMatched`, score increases by one, and they stay face-up.
  - If they don't match, both flip back after a short delay.
- A move is counted each time a second card is flipped for comparison.
- The game is complete when every card has been matched.

## What I Learned

This project was built to go deeper on React state management:

- Extracting game logic into a custom hook, separate from UI components
- Updating arrays of objects immutably (`map`, spread) rather than mutating state directly
- Lazy `useState` initializers for one-time setup work, instead of reaching for `useEffect`
- Functional state updates (`setScore(prev => prev + 1)`) to avoid stale-state bugs
- Using `setTimeout` alongside React state to create a timed flip-back effect
- Parent/child communication via props — `Card` reports clicks upward, `App`/the hook decides what they mean


## Future Improvements

- Difficulty levels (more pairs, different grid sizes)
- Persist best score/moves with `localStorage`
- Flip animation (CSS transform) instead of an instant swap
- Timer-based scoring mode
