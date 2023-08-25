using JetBrains.Annotations;
using System;
using UnityEngine;

namespace Chess.Scripts.Core {

    public class ChessPlayerPlacementHandler : MonoBehaviour {
        [SerializeField] public int row, column;
        public int printRow, printColumn;

        public GameObject GameManager;

        bool checkBlocked = false;

        private void Start() {
            transform.position = ChessBoardPlacementHandler.Instance.GetTile(row, column).transform.position;
        }

        private void OnMouseDown()
        {
            ChessBoardPlacementHandler.Instance.ClearHighlights();
            GameManager.GetComponent<GameManager>().selectedPiece = gameObject;
            HighlightPossibleMoves();
        }

        public void HighlightPossibleMoves()
        {
            GameObject currentSelectedPiece = GameManager.GetComponent<GameManager>().selectedPiece;

            if (GameManager.GetComponent<GameManager>().selectedPiece != null)
            {
                if (currentSelectedPiece.CompareTag("Queen")) Queen();
                else if (currentSelectedPiece.CompareTag("Rook")) Rook();
                else if (currentSelectedPiece.CompareTag("Bishop")) Bishop();
                else if (currentSelectedPiece.CompareTag("Pawn")) Pawn();
                else if (currentSelectedPiece.CompareTag("King")) King();
                else if (currentSelectedPiece.CompareTag("Knight")) Knight();
            }
        }

        public void Queen()
        {
            DiagonalMoves();
            VerticalMoves();
            HorizontalMoves();
        }

        public void Bishop()
        {
            DiagonalMoves();
        }

        public void Rook()
        {
            VerticalMoves();
            HorizontalMoves();
        }

        public void Pawn()
        {
            OneMoveFront();
        }

        public void King()
        {
            OneMoveAllSide();
        }

        public void Knight()
        {
            printRow = row - 2;
            printColumn = column - 1;

            for(int i = 0; i < 2; i++){
                printColumn = column - 1;
                for (int j = 0; j < 2; j++){
                    if (InChessBoundaries()) HighlightValid();
                    printColumn += 2;
                }
                printRow = row + 2;
            }

            printRow = row - 1;
            printColumn = column - 2;

            for (int i = 0; i < 2; i++) {
                printRow = row - 1;
                for (int j = 0; j < 2; j++) {
                    if (InChessBoundaries()) HighlightValid();
                    printRow += 2;
                }
                printColumn = column + 2;
            }
        }

        public void OneMoveFront()
        {
            printRow = row + 1;
            printColumn = column;

            if (InChessBoundaries()) HighlightValid();
        }

        public void OneMoveAllSide()
        {
            printRow = row - 1;
            printColumn = column - 1;

            for (; printRow < row + 2; printRow++)
            {
                for (printColumn = column - 1; printColumn < column + 2; printColumn++)
                {
                    if (InChessBoundaries()) HighlightValid();
                }
            }
        }

        public void DiagonalMoves()
        {
            // Debug.Log("Diagonal Moves was called");

            printRow = row + 1;
            printColumn = column + 1;

            checkBlocked = false;

            while (InChessBoundaries())
            {
                if (checkBlocked) break;
                else HighlightValid();
                printRow++; printColumn++;
            }

            printRow = row + 1;
            printColumn = column - 1;

            checkBlocked = false;

            while (InChessBoundaries())
            {
                if (checkBlocked) break;
                else HighlightValid();

                printRow++; printColumn--;
            }

            printRow = row - 1;
            printColumn = column + 1;

            checkBlocked = false;

            while (InChessBoundaries())
            {
                if (checkBlocked) break;
                else HighlightValid();

                printRow--; printColumn++;
            }

            printRow = row - 1;
            printColumn = column - 1;

            checkBlocked = false;

            while (InChessBoundaries())
            {

                if (checkBlocked) break;
                else HighlightValid();

                printRow--; printColumn--;
            }
        }

        public void VerticalMoves()
        {
            // Debug.Log("Vertical Moves was called");

            printRow = row + 1;
            printColumn = column;

            checkBlocked = false;

            while (InChessBoundaries())
            {
                if (checkBlocked) break;
                else HighlightValid();

                printRow++;
            }

            printRow = row - 1;
            checkBlocked = false;

            while (InChessBoundaries())
            {
                if (checkBlocked) break;
                else HighlightValid();
                printRow--;
            }
        }

        public void HorizontalMoves()
        {
            // Debug.Log("Horizontal Moves was called");

            printRow = row;
            printColumn = column + 1;

            checkBlocked = false;

            while (InChessBoundaries())
            {
                if (checkBlocked) break;
                else HighlightValid();
                printColumn++;
            }

            printColumn = column - 1;
            checkBlocked = false;

            while (InChessBoundaries())
            {
                if (checkBlocked) break;
                else HighlightValid();
                printColumn--;
            }
        }

        public void HighlightValid()
        {
            GameObject playerPositions = GameObject.Find("Player Positions");

            for (int i = 0; i < playerPositions.transform.childCount; i++)
            {
                GameObject child = playerPositions.transform.GetChild(i).gameObject;

                if (child.GetComponent<ChessPlayerPlacementHandler>().row == printRow && 
                    child.GetComponent<ChessPlayerPlacementHandler>().column == printColumn)
                {
                    checkBlocked = true;
                    return;
                }
            }
            ChessBoardPlacementHandler.Instance.Highlight(printRow, printColumn);
            
            // Debug.Log("Highlight was called");
        }

        public bool InChessBoundaries()
        {
            return (printRow >= 0) && (printRow < 8) && (printColumn >= 0) && (printColumn < 8);
        }
    }
}
