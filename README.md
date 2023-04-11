# thyhuynh
<!DOCTYPE html>
<html>

<head>
    <title> Co_Caro </title>
    <script src="https://unpkg.com/react@18/umd/react.development.js" crossorigin></script>
    <script src="https://unpkg.com/react-dom@18/umd/react-dom.development.js" crossorigin>
    </script>
    <script src="https://unpkg.com/@babel/standalone/babel.min.js"></script>
</head>
<style>
    body {
        font: 34px "Century Gothic", Futura, sans-serif;
        margin: 520px;
        margin-top: 200px;
    }

    .square {
        background: #fff;
        border: 1.5px solid black;
        float: left;
        font-size: 54px;
        font-weight: bold;
        line-height: 64px;
        height: 64px;
        margin-right: -1px;
        margin-top: -1px;
        padding: 0;
        text-align: center;
        width: 64px;
    }

    .board-row::after {
        clear: both;
        content: "";
        display: table;
    }
    .status{
        font-size:25px;
        margin-left:10px;
        padding-bottom: 10px;
        font-weight: bold;
    }
</style>

<body>
    <div id="mydiv"></div>
    <script type="text/babel">
        function Square({ ox, onClick }) {
            return (
                <button className="square" onClick={onClick}>{ox}</button>
            )
        }
        function Board() {
            const [xIsNext, setXIsNext] = React.useState(true);
            const [squares, setSquares] = React.useState(Array(9).fill(null));
            function handleClick(i) {
                if (squares[i] || checkWinner(squares)) {
                    return;
                }
                const nextSquares = squares.slice();
                xIsNext % 2 === 0 ? nextSquares[i] = "O" : nextSquares[i] = "X";
                setSquares(nextSquares);
                setXIsNext(!xIsNext);
            }
            const winner = checkWinner(squares);
            let status;
            if (winner) {
                status = 'Winner: ' + winner;
            } else {
                status = 'Next player: ' + (xIsNext ? 'X' : 'O');
            }
            return (
                <>
                    <div className="status">{status}</div>
                    <div className="board-row">
                        <Square ox={squares[0]} onClick={() => handleClick(0)} />
                        <Square ox={squares[1]} onClick={() => handleClick(1)} />
                        <Square ox={squares[2]} onClick={() => handleClick(2)} />
                    </div>
                    <div className="board-row">
                        <Square ox={squares[3]} onClick={() => handleClick(3)} />
                        <Square ox={squares[4]} onClick={() => handleClick(4)} />
                        <Square ox={squares[5]} onClick={() => handleClick(5)} />
                    </div>
                    <div className="board-row">
                        <Square ox={squares[6]} onClick={() => handleClick(6)} />
                        <Square ox={squares[7]} onClick={() => handleClick(7)} />
                        <Square ox={squares[8]} onClick={() => handleClick(8)} />

                    </div>
                </>
            );
        }

        function checkWinner(squares) {
            const lines = [
                [0, 1, 2],
                [3, 4, 5],
                [6, 7, 8],
                [0, 3, 6],
                [1, 4, 7],
                [2, 5, 8],
                [0, 4, 8],
                [2, 4, 6],
            ];
            for (let i = 0; i < lines.length; i++) {
                const [a, b, c] = lines[i];
                if (squares[a] && squares[a] === squares[b] && squares[a] === squares[c]) {
                    return squares[a];
                }
            }
            return null;
        }
        ReactDOM.render(<Board />, document.getElementById('mydiv'))
    </script>
</body>

</html>
