import React, { useState, useEffect } from "react"; import { Button } from "@/components/ui/button";

const BOARD_SIZE = 10; const SHIPS = [5, 4, 3, 3, 2];

const createEmptyBoard = () => Array.from({ length: BOARD_SIZE }, () => Array(BOARD_SIZE).fill(""));

const placeShipsRandomly = () => { const board = createEmptyBoard(); for (const size of SHIPS) { let placed = false; while (!placed) { const horizontal = Math.random() > 0.5; const row = Math.floor(Math.random() * BOARD_SIZE); const col = Math.floor(Math.random() * BOARD_SIZE); let fits = true;

for (let i = 0; i < size; i++) {
    const r = row + (horizontal ? 0 : i);
    const c = col + (horizontal ? i : 0);
    if (r >= BOARD_SIZE || c >= BOARD_SIZE || board[r][c] === "S") {
      fits = false;
      break;
    }
  }

  if (fits) {
    for (let i = 0; i < size; i++) {
      const r = row + (horizontal ? 0 : i);
      const c = col + (horizontal ? i : 0);
      board[r][c] = "S";
    }
    placed = true;
  }
}

} return board; };

const GameBoard = () => { const [enemyBoard, setEnemyBoard] = useState(placeShipsRandomly()); const [hits, setHits] = useState(createEmptyBoard)
